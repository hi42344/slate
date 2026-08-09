```cpp
// Metadata defining the file properties sent
struct FileHeader {
    name;
    size;
    path;
}

// Defining the port we're going to use
var port__ = 9000;

// Asynchronously packages the file header metadata and payload into a single stream packet
fn async_send_file(sock, file_data, name, path, callback) {
    if (!net.tcp.is_open(sock)) {
        callback(false);
        return null;
    }

    // Serialize header metadata into a JSON string
    var header_struct = FileHeader(name, file_data.length, path);
    var header_json = json.stringify(header_struct);
    
    // Construct the packet layout: [Header Length]\n[JSON Header][Compressed Data]
    var full_packet = "" + header_json.length + "\n" + header_json + file_data;

    net.tcp.async_send(sock, full_packet, fn(ok) {
        callback(ok);
    });
}

// Utility function to parse cmd flags, eg: "data=hello_world"
fn find_value_of_arg(prefix) {
    var full_prefix = prefix;
    if (string.sub(prefix, prefix.length - 1, prefix.length - 1) != "=") {
        full_prefix = prefix + "=";
    }

    var args = os.args();
    for (var i = 0; i < args[0]; i += 1) {
        var arg = args[1][i];
        if (arg.length >= full_prefix.length) {
            var arg_head = string.sub(arg, 0, full_prefix.length - 1);
            if (arg_head == full_prefix) {
                return string.sub(arg, full_prefix.length, arg.length - 1);
            }
        }
    }

    return null;
}

var running = true;

// Get the inputs with fallbacks
var data___ = find_value_of_arg("data");
var file_name__ = find_value_of_arg("name");

if (!data___) {
    data___ = "ERROR";
}
if (!file_name__) {
    file_name__ = "ERROR.txt";
}

print("Connecting to server");

// Starting the connection with the port 
net.tcp.async_connect("127.0.0.1", port__, fn(sock) {
    if (sock == 0) {
        print("Failed to connect to server.");
        running = false;
        return null;
    }

    print("Connected. Sending payload");
    var file_name = file_name__;
    var folder_path = "C:\\Developer\\slate\\NETWORK_SERVER_FILE";
    
    // Compress using deflate for network optimization
    var payload = compression.deflate_compress(data___, 6);

    async_send_file(sock, payload, file_name, folder_path, fn(ok) {
        if (ok) {
            print("File sent to network queue.");
        } else {
            print("Failed to send file.");
        }
        net.tcp.close(sock);
        running = false;
    });
});

// Main event loop
while (running) {
    net.poll();
}
```
