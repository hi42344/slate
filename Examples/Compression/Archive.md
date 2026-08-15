# A .spak archive format #

**A O(1) random access (besides traversing the archive which is O(n) but that is so fast that it mostly doesn't matter) archiving format** 

```rust
// Automatically selects the best compression algorithm based on file type and size
fn select_codec(file_path, raw_size) {
    var ext = string.lower(os.file_extension(file_path));

    // Skip compression for already-compressed media, archives, fonts, and transient build artifacts
    if (ext == ".png" || ext == ".jpg" || ext == ".jpeg" || ext == ".webp" || ext == ".ico" ||
        ext == ".mp3" || ext == ".flac" || ext == ".ogg" || ext == ".mp4" ||
        ext == ".zip" || ext == ".7z" || ext == ".rar" || ext == ".tar" || ext == ".gz" || ext == ".xz" ||
        ext == ".ttf" || ext == ".otf" || ext == ".woff" || ext == ".woff2" ||
        ext == ".lib" || ext == ".a" || ext == ".obj" || ext == ".o" || 
        ext == ".pdb" || ext == ".ilk" || ext == ".pch" || ext == ".suo" || ext == ".sdf") {
        return "store";
    }

    // Route large files (> 65MB) to LZMA, keeping smaller files and non exe/dll files on Zstd
    if (raw_size > 68157440 && ext != ".exe" && ext != ".dll") {
        return "lzma";
    }

    // Route small temporary or diagnostic files to LZ4 for speed
    if (ext == ".log" || ext == ".tmp" || ext == ".cache" || 
        ext == ".csv" || ext == ".jsonl" || ext == ".dmp" || ext == ".crash") {
        return "lz4";
    }

    // Default
    return "zstd";
}

// Helper to strip the base directory and get a clean relative path
fn get_relative_path(file_path, base_dir) {
    var base_len = base_dir.length;
    var rel = file_path;
    
    // Only attempt to trim if the file path is longer than the base directory path
    if (file_path.length > base_len) {
        // Check the character immediately following the base path
        var char_at = string.sub(file_path, base_len, base_len);
        var start_idx = base_len;
        
        // If there is a trailing slash or backslash, skip past it to avoid a leading slash in the result
        if (char_at == "\\" || char_at == "/") {
            start_idx = base_len + 1;
        }
        
        // Extract the remaining portion of the string as the relative path
        rel = string.sub(file_path, start_idx, file_path.length - 1);
    }
    
    return rel;
}

// Packs an array of file paths into an archive file with a manifest and compressed payload
fn pack_files(file_paths, output_archive_path, base_dir) {
    var manifest = ""; 
    var payload_chunks = []; // Array to collect chunks efficiently
    var current_offset = 0;  // Tracks running byte position
    
    for (var i = 0; i < file_paths.length; i = i + 1) {
        var file_path = file_paths[i];
        
        if (!os.file_exists(file_path) || !os.is_file(file_path)) {
            continue;
        }

        var raw_data = os.file_load(file_path);
        if (type.is_null(raw_data)) {
            continue;
        }

        var orig_size = raw_data.length;
        var codec = select_codec(file_path, orig_size);
        var compressed = raw_data;

        if (codec == "lzma") {
            compressed = compression.lzma_compress(raw_data, 5); 
        } elif (codec == "zstd") {
            compressed = compression.zstd_compress(raw_data, 3);
        } elif (codec == "deflate") {
            compressed = compression.deflate_compress(raw_data, 6);
        } elif (codec == "lz4") {
            compressed = compression.lz4_compress(raw_data, 0);
        }

        var offset = current_offset;
        var comp_size = compressed.length;

        // Push chunk to array
        payload_chunks.push(compressed);
        current_offset = current_offset + comp_size;

        var rel_path = get_relative_path(file_path, base_dir);

        manifest = manifest + rel_path + "|" + codec + "|" + 
                    type.to_string(offset) + "|" + 
                    type.to_string(comp_size) + "|" + 
                    type.to_string(orig_size) + "\n";
    }

    // Join all accumulated chunks together
    var payload = string.join(payload_chunks, "");

    var header = "SLATEPAK_V3\n" + manifest + "---DATA---\n";
    var full_archive = header + payload;

    var archive_dir = os.path_dirname(output_archive_path);
    if (archive_dir.length > 0 && !os.file_exists(archive_dir)) {
        if (!os.mkdir(archive_dir)) {
            return false;
        }
    }

    var saved = os.file_save(output_archive_path, full_archive);
    if (!saved) {
        return false;
    }

    return true;
}

// Unpacks all files stored inside an archive into a target output directory
fn unpack_files(archive_path, output_directory) {
    // Validate archive exists
    if (!os.file_exists(archive_path)) {
        return false;
    }
    
    // Load the entire archive into memory
    var archive_data = os.file_load(archive_path);
    if (type.is_null(archive_data)) {
        return false;
    }

    // Locate the boundary between the readable manifest and the binary payload
    var header_delimiter = "---DATA---\n";
    var delimiter_pos = string.find(archive_data, header_delimiter);
    if (delimiter_pos == -1) {
        return false; // Malformed archive, missing data section
    }

    // Ensure the base destination directory exists before extracting
    if (!os.file_exists(output_directory)) {
        if (!os.mkdir(output_directory)) {
            return false;
        }
    }

    // Calculate where the actual file bytes begin
    var payload_start_offset = delimiter_pos + header_delimiter.length;
    
    // Extract just the manifest portion and split it into individual file records
    var header_text = string.sub(archive_data, 0, delimiter_pos - 1);
    var lines = string.split(header_text, "\n");

    // Loop through the manifest lines (starting at 1 to skip the "SLATEPAK_V3" header)
    for (var i = 1; i < lines.length; i = i + 1) {
        var line = lines[i];
        if (line.length == 0) { continue; } // Skip empty lines

        // Parse the metadata fields separated by the pipe character
        var parts = string.split(line, "|");
        var rel_path = parts[0];
        var codec = parts[1];
        var offset = type.string_to_number(parts[2]);
        var comp_size = type.string_to_number(parts[3]);
        var orig_size = type.string_to_number(parts[4]);

        // Calculate the absolute position of this file's chunk in the overall archive string
        var abs_offset = payload_start_offset + offset;
        var compressed_chunk = string.sub(archive_data, abs_offset, abs_offset + comp_size - 1);

        // Route the compressed chunk to the correct decompression algorithm
        var decompressed = compressed_chunk;
        if (codec == "lzma") {
            decompressed = compression.lzma_decompress(compressed_chunk);
        } elif (codec == "zstd") {
            decompressed = compression.zstd_decompress(compressed_chunk);
        } elif (codec == "deflate") {
            decompressed = compression.deflate_decompress(compressed_chunk);
        } elif (codec == "lz4") {
            decompressed = compression.lz4_decompress(compressed_chunk);
        }

        // Reconstruct the intended extraction path combining the base dir and relative path
        var destination = os.path_join(output_directory, rel_path);
        var dest_dir = os.path_dirname(destination);
        
        // Make sure all required nested subdirectories exist before trying to write the file
        if (!os.file_exists(dest_dir)) {
            os.mkdir(dest_dir);
        }

        // Write the decompressed file to disk
        var saved = os.file_save(destination, decompressed);
        if (!saved) {
            return false;
        }
    }

    return true;
}

// Extracts and returns a single file's content from the archive without unpacking everything
fn get_single_file(archive_path, target_file_name, base_dir) {
    if (!os.file_exists(archive_path)) {
        return false;
    }
    
    var archive_data = os.file_load(archive_path);
    if (type.is_null(archive_data)) {
        return false;
    }

    // Locate the payload boundary
    var header_delimiter = "---DATA---\n";
    var delimiter_pos = string.find(archive_data, header_delimiter);
    if (delimiter_pos == -1) {
        return false;
    }

    // Normalize the requested target string to a relative path just in case the user passed an absolute path
    var search_target = target_file_name;
    if (base_dir && target_file_name.length >= base_dir.length) {
        var base_len = base_dir.length;
        var char_at = string.sub(target_file_name, base_len, base_len);
        var start_idx = base_len;
        if (char_at == "\\" || char_at == "/") {
            start_idx = base_len + 1;
        }
        search_target = string.sub(target_file_name, start_idx, target_file_name.length - 1);
    }

    var payload_start_offset = delimiter_pos + header_delimiter.length;
    var header_text = string.sub(archive_data, 0, delimiter_pos - 1);
    var lines = string.split(header_text, "\n");

    // Scan the manifest to find the specific requested file
    for (var i = 1; i < lines.length; i = i + 1) {
        var line = lines[i];
        if (line.length == 0) { continue; }

        var parts = string.split(line, "|");
        var rel_path = parts[0];
        var codec = parts[1];
        var offset = type.string_to_number(parts[2]);
        var comp_size = type.string_to_number(parts[3]);
        var orig_size = type.string_to_number(parts[4]);

        var filename = os.path_filename(rel_path);
        
        // Check if the current manifest entry matches the exact relative path, normalized path, or raw filename
        if (rel_path == target_file_name || rel_path == search_target || filename == target_file_name) {
            
            // Extract only the isolated chunk belonging to this file
            var abs_offset = payload_start_offset + offset;
            var compressed_chunk = string.sub(archive_data, abs_offset, abs_offset + comp_size - 1);

            // Decompress the isolated chunk
            var decompressed = compressed_chunk;
            if (codec == "lzma") {
                decompressed = compression.lzma_decompress(compressed_chunk);
            } elif (codec == "zstd") {
                decompressed = compression.zstd_decompress(compressed_chunk);
            } elif (codec == "deflate") {
                decompressed = compression.deflate_decompress(compressed_chunk);
            } elif (codec == "lz4") {
                decompressed = compression.lz4_decompress(compressed_chunk);
            }

            // Return the uncompressed raw bytes of the single file directly to the caller
            return decompressed;
        }
    }

    return false; // File was not found in the archive
}

//A all_files function for getting all files from a directory 
fn all_files(base_dir) {
    var files = [];
    var dir_list = os.dir_list(base_dir);
    
    for (var i = 0; i < dir_list.length; i += 1) {
        var path = os.path_join(base_dir, dir_list[i]);
        
        if (os.is_dir(path)) {
            var sub_files = all_files(path);
            
            for (var j = 0; j < sub_files.length; j += 1) {
                files.push(sub_files[j]);
            }
        } else {
            files.push(path);
        }
    }
    
    return files;
}

var base_dir = "Placeholder";

var files = all_files(base_dir);

var archive_file = os.path_join(base_dir, "Archive.spak");
var extract_folder = os.path_join(base_dir, "Extracted");

// 1. Making the archive
pack_files(files, archive_file, base_dir);

// 2. Extract a single file directly from the archive
var target_file_name = "Placeholder.Placeholder"; 
var single_file_bytes = get_single_file(archive_file, target_file_name, base_dir);

if (single_file_bytes != false) {
    var single_save_path = os.path_join(base_dir, "Placeholder.Placeholder");
    os.file_save(single_save_path, single_file_bytes);
}

// Note that decompressing/extracting is much faster compared to compressing/making an archive
unpack_files(archive_file, extract_folder);
```
