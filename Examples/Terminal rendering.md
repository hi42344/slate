```cpp
fn render_terminal_image(path) {
    var img = image.load(path);
    if (img == -1) {
        console.out("Failed to load image: " + path + "\n");
        return -1;
    }

    var target_w = console.width();
    //Getting the correct aspect ratio with * 2 (1 terminal character is about 1:2 aspect ratio)
    var target_h = (console.height() - 1) * 2;

    if (target_w <= 0) { target_w = 1; }
    if (target_h <= 0) { target_h = 2; }

    //The correctly scale image
    var scaled = image.resize(img, target_w, target_h);

    //Buffer
    var frame = "";

    for (var y = 0; y < target_h; y = y + 2) {
        var line = "";
        for (var x = 0; x < target_w; x = x + 1) {
            var p1 = image.get_pixel(scaled, x, y);
            var r1 = p1[0];
            var g1 = p1[1];
            var b1 = p1[2];

            var r2 = 0; var g2 = 0; var b2 = 0;
            if (y + 1 < target_h) {
                var p2 = image.get_pixel(scaled, x, y + 1);
                r2 = p2[0];
                g2 = p2[1];
                b2 = p2[2];
            }

            //Setting the color and putting the correct half-block
            line += "\x1b[38;2;" + r1 + ";" + g1 + ";" + b1 + "m" +
                          "\x1b[48;2;" + r2 + ";" + g2 + ";" + b2 + "m▀";
        }
        //Adding the line to the frame
        frame += line + "\x1b[0m\n";
    }

    //The actual rendering
    console.command(frame);

    //Cleanup
    image.free(img);
    image.free(scaled);
}

//Go to the libraries image documentation example
var path = "output.png";

var last_console_width = console.width();
var last_console_height = console.height();
render_terminal_image(path);

while(!input.is_key_down("escape")) {
    //Make sure to not render again if the console width and height are the same 
    if(console.width() != last_console_width || console.height() != last_console_height) {
        last_console_width = console.width();
        last_console_height = console.height();
        //Clearing for the new image
        console.clear();
        //Rendering
        render_terminal_image(path);
        os.sleep(0.05);
    }
    else {
        //Polling if not the same
        os.sleep(0.01);
    }
}
```
