### A basic server that connects to clients (go in Client.md for the client-side)
```cpp
// Structure representing the fully received and parsed file payload data
struct FileResult {
    name;
    size;
    data;
    path;
}

// Helper function to parse integer values
fn parse_int(str) {
    var result = 0;
    var i = 0;
    while (i < str.length) {
        var code = string.charCode(str, i);
        result = (result * 10) + (code - 48);
        i = i + 1;
    }
    return result;
}

// Scans for a newline character to delimit stream lengths
fn find_newline(str) {
    var i = 0;
    while (i < str.length) {
        if (string.charCode(str, i) == 10) {
            return i;
        }
        i = i + 1;
    }
    return -1;
}

// Asynchronously reads chunks and processes them using a state machine
fn async_load_file(sock, callback) {
    var buffer = "";
    var state = "READ_LEN"; // Parsing States (READ_LEN -> READ_HEADER -> READ_PAYLOAD)
    var header_len = 0;
    var header = null;

    fn receive_step() {
        net.tcp.async_recv(sock, 4096, fn(chunk) {
            if (chunk == "") {
                callback(null);
                return null;
            }

            buffer = buffer + chunk;

            var processing = true;
            while (processing) {
                processing = false;

                // State 1: Read the header length prefix delimited by a newline character
                if (state == "READ_LEN") {
                    var nl_idx = find_newline(buffer);
                    if (nl_idx != -1) {
                        var len_prefix = "";
                        if (nl_idx > 0) {
                            len_prefix = string.sub(buffer, 0, nl_idx - 1);
                        }
                        
                        buffer = string.sub(buffer, nl_idx + 1, -1);
                        header_len = parse_int(len_prefix);
                        state = "READ_HEADER";
                        processing = true;
                    }
                // State 2: Read the JSON-encoded metadata header string based on its length
                } elif (state == "READ_HEADER") {
                    if (buffer.length >= header_len) {
                        var header_json = string.sub(buffer, 0, header_len - 1);
                        buffer = string.sub(buffer, header_len, -1);
                        header = json.parse(header_json);

                        if (header == null) {
                            print("Error: Malformed header JSON.");
                            callback(null);
                            return null;
                        }

                        state = "READ_PAYLOAD";
                        processing = true;
                    }
                // State 3: Read the raw file payload based on the size specified in the header
                } elif (state == "READ_PAYLOAD") {
                    if (buffer.length >= header.size) {
                        var file_payload = string.sub(buffer, 0, header.size - 1);
                        buffer = string.sub(buffer, header.size, -1);

                        callback(FileResult(header.name, header.size, file_payload, header.path));
                        return null;
                    }
                }
            }

            if (net.tcp.is_open(sock)) {
                receive_step();
            }
        });
    }

    receive_step();
}

// Defining the port we're going to start the server on
var port = 9000;
// Making the listener 
var listener = net.tcp.listen(port);

if (listener == 0) {
    print("ERROR: Could not bind to port " + port + ". Port is occupied or in TIME_WAIT.");
} else {
    print("Server successfully listening on port " + port);

    var running = true;

    fn accept_loop() {
        net.tcp.async_accept(listener, fn(client_sock) {
            accept_loop();

            if (client_sock != 0) {
                print("\nClient connected. Receiving file");

                async_load_file(client_sock, fn(file_info) {
                    if (file_info != null) {
                        // Decompress the payload using deflate
                        file_info.data = compression.deflate_decompress(file_info.data);
                        print("-- Loaded --");
                        print("File Name: \"" + file_info.name + "\"");
                        print("File Size: " + file_info.size + " bytes");
                        print("Folder Path: \"" + file_info.path + "\"");
                        print("Data: \"" + file_info.data + "\"");
                    } else {
                        print("Transfer failed or client disconnected.");
                    }

                    // Make sure the directory exists
                    if (file_info != null && !os.file_exists(file_info.path)) {
                        os.mkdir(file_info.path);
                        print("Made directory: \"" + file_info.path + "\"");
                    }

                    // Save the processed file to disk
                    if (file_info != null) {
                        var save_path = os.path_join(file_info.path, file_info.name);
                        os.file_save(save_path, file_info.data);
                        print("Saved \"" + file_info.name + "\" at \"" + save_path + "\"");
                    }

                    net.tcp.close(client_sock);
                    print("\n-- Connection closed --\n");
                });
            }
        });
    }

    accept_loop();

    // Main event loop
    while (running) {
        net.poll();
        //For tiny inputs so they dont show nothing
        console.flush();
    }

    net.tcp.stop_listen(listener);
}
```
