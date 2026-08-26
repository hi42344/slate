# Core libraries #
 
### Table of Contents
 
| Library | Description |
| :--- | :--- |
| [**Math**](#math) | Math |
| [**OS**](#os) | File, clock, times |
| [**File**](#file) | Streamed file utilities |
| [**Input**](#input) | Keyboard and Mouse utilities |
| [**Data**](#data) | Easy data saving |
| [**Coroutine**](#coroutine) | Concurrency |
| [**Memory**](#memory) | memory utilities |
| [**Bitwise**](#bitwise) | Bitwise operations |
| [**Compression**](#compression) | compression utilities |
| [**Networking**](#net) | Networking utilities |
| [**Json**](#json) | json utilities |
| [**Console**](#console) | console utilities |
| [**Image**](#image) | Image utilities |
| [**Color**](#color) | color utilities |
| [**Audio**](#audio) | Audio utilities |
| [**String**](#string) | String and hashing utilities |
| [**Array**](#array) | Array utilities |
| [**Class**](#class) | Class information |
| [**Struct**](#struct) | Struct information |
| [**Type**](#type) | Type checking and casting |
| [**Slate**](#slate) | Language utilities/info |

- ```print(contents)``` // prints whatever is in it, eg: ```print("hello world" + 5);``` this prints "hello world5" and a new line.

**Added in v0.4.0**
- ```try(function)``` // Returns a struct with .result **(the return value)**, and .error **(Is the error code on failure (null if no failure), is "Unknown error" if the error is not a standard exception or RuntimeError)**. **(If pointers are made inside of the try block they will leak, even things with deconstructors, this is not like a try catch, it's like a lua pcall)**. 
**E.g.,**
```slate
//The function can't have any arguments
var result_struct = try(fn() {
    var error_arr = [1, 2, 3, 4, 5];
    return error_arr[100];
});

//Error isnt null
if(result_struct.error) {
    //Result is null if error
    print("Error = \"" + result_struct.error + "\"");
}
else {
   print("No error, result = \"" + result_struct.result + "\"");
}
```

# Math #
- ```math.abs(number)``` // Returns the absolute value of a number
- ```math.acos(number)``` // Returns the arc cosine of a number in radians
- ```math.asin(number)``` // Returns the arc sine of a number in radians
- ```math.atan(number)``` // Returns the arc tangent of a number in radians
- ```math.atan2(y, x)``` // Returns the arc tangent of y/x in radians using signs to determine the quadrant
- ```math.ceil(number)``` // Rounds a number upward to the nearest integer
- ```math.cos(number)``` // Returns the cosine of an angle in radians
- ```math.cosh(number)``` // Returns the hyperbolic cosine of a number
- ```math.deg(radians)``` // Converts an angle from radians to degrees
- ```math.exp(number)``` // Returns e raised to the power of a number
- ```math.floor(number)``` // Rounds a number downward to the nearest integer
- ```math.fmod(x, y)``` // Returns the floating-point remainder of x/y
- ```math.huge()``` // Returns positive infinity
- ```math.log(number)``` // Returns the natural logarithm (base e) of a number
- ```math.log10(number)``` // Returns the common logarithm (base 10) of a number
- ```math.max(x, y)``` // Returns the larger of two values
- ```math.min(x, y)``` // Returns the smaller of two values
- ```math.pi()``` // Returns the mathematical constant pi (3.14159265358979323846)
- ```math.pow(base, exp)``` // Returns the base raised to the power of the exponent
- ```math.rad(degrees)``` // Converts an angle from degrees to radians
- ```math.sin(number)``` // Returns the sine of an angle in radians
- ```math.sinh(number)``` // Returns the hyperbolic sine of a number
- ```math.sqrt(number)``` // Returns the square root of a number
- ```math.tan(number)``` // Returns the tangent of an angle in radians
- ```math.tanh(number)``` // Returns the hyperbolic tangent of a number
- ```math.random(min, max)``` // Generates a pseudo-random double between min and max
- ```math.random_seeded(min, max, seed)``` // Generates a pseudo-random double between min and max using a seed
- ```math.sign(number)``` // Returns 1 for positive, -1 for negative, or 0 for zero
- ```math.clamp(value, min, max)``` // Restricts a value to be between a minimum and maximum range
- ```math.round(number)``` // Rounds a number to the nearest integer
- ```math.lerp(a, b, t)``` // Linearly interpolates between a and b by t
- ```math.map(value, in_min, in_max, out_min, out_max)``` // Linearly maps a value from an input range to an output range
- ```math.noise(x, y, z)``` // Generates 3D Perlin noise based on the input coordinates x, y, and z

**Added in v0.2.0**
- ```math.random_int(min, max)``` // Same as math.random(min, max) but returns a integer
- ```math.e()``` // Returns Euler's number `e` (2.71828182845904523536)
- ```math.log2(number)``` // Returns the base-2 logarithm of a number
- ```math.cbrt(number)``` // Returns the cube root of a number
- ```math.hypot(x, y)``` // Returns the hypotenuse sqrt(x*x + y*y) avoiding intermediate overflow
- ```math.distance(x1, y1, x2, y2)``` // Returns the Euclidean distance between two 2D points
- ```math.fract(number)``` // Returns the fractional part of a number (number - floor(number))
- ```math.mod(x, y)``` // Returns the floor remainder of x/y, properly wrapping negative numbers
- ```math.sind(degrees)``` // Returns the sine of an angle in degrees
- ```math.cosd(degrees)``` // Returns the cosine of an angle in degrees
- ```math.tand(degrees)``` // Returns the tangent of an angle in degrees
- ```math.atan2d(y, x)``` // Returns the arc tangent of y/x in degrees
- ```math.angle_difference(a, b)``` // Returns the shortest signed angular difference between two angles in degrees (-180 to 180)
- ```math.lerp_angle(a, b, t)``` // Linearly interpolates between two angles in degrees along the shortest path
- ```math.inverse_lerp(a, b, value)``` // Calculates the linear parameter t that produces the interpolant value between a and b
- ```math.smoothstep(min, max, x)``` // Performs smooth Hermite interpolation between 0 and 1 when x is between min and max

**Added in v0.3.0**
- ```math.factorial(n)``` // Returns a string of the factorial of n (Uses Boost-GMP)
- ```math.fibonacci(n)``` // Returns a string of the fibonacci of n (Uses Boost-GMP)
- ```math.is_prime(n)``` // Returns either true or false if `n` is prime (Uses Miller-Rabin)
- ```math.gcd(a, b)``` // Returns the greatest common divisor of `a` and `b` (Throws an error if either is `-9223372036854775808`)
- ```math.lcm(a, b)``` // Returns the least common multiple of `a` and `b` (Throws an error on overflow or if either is `-9223372036854775808`)

# Os #
- ```os.sleep(time)``` // sleeps the program for the time in seconds
- ```os.throw(message)``` // throws/crashes the program and prints the message
- ```os.platform()``` // Returns the current platform, eg: **```"windows", "linux", "macos", "ios", "android"```** else **```"unknown"```**
- ```os.time()``` // Returns the current UTC Unix timestamp (in seconds) since the epoch (Jan 1, 1970). Best for calendar dates and wall-clock timestamps.
- ```os.clock()``` // Returns high-precision elapsed time (in seconds) since the program started
- ```os.date()``` // Returns a **locally formatted string** of the current date and time
- ```os.date_time_year()``` // Returns the current time and year formatted as **"Hours:Minutes:Seconds Year"**
- ```os.date_time()``` // Returns the current time formatted as **"Hours:Minutes:Seconds"**
- ```os.getenv(env_var)``` // Returns the value of an **environment variable**, or an empty string if not found
- ```os.file_save(path, content)``` // Saves content to a file **(overwriting if it exists)**, returns true if successful
- ```os.file_load(path)``` // Returns the **entire contents** of a file as a **string**
- ```os.file_exists(path)``` // Returns true if a **file or directory** exists at the path, otherwise false
- ```os.file_delete(path)``` // Deletes a **file or empty directory**, returns true if successful
- ```os.file_size(path)``` // Returns the **size of a file in bytes**, or -1 if the file is not found
- ```os.file_append(path, content)``` // Appends content to the **end of a file**, returns true if successful

**Added in v0.2.0**
- ```os.input(prompt)``` // gets user input using ```std::getline()```
- ```os.uuid()``` // Returns a randomly generated **RFC 4122 version-4 UUID** as a string, eg: ```"f47ac10b-58cc-4372-a567-0e02b2c3d479"```
- ```os.exit(exit_code)``` // Uses ```std::exit(exit_code)```

**Added in v0.3.0**
- ```os.load_plugin(path)``` // Loads a plugin/dynamic library, allowing you to use its functions
- ```os.dir_list(path)``` // Returns an array of file/folder names inside a specified directory
- ```os.file_extension(path)``` // Returns somethings file extension, eg: `file.png` -> ".png", `file.txt` -> ".txt", note that *multi-extension* things will only give the last extension, eg: `file.tar.gz` -> ".gz"
- ```os.path_join(a, b)``` // Joins two path segments using the correct platform-specific separator
- ```os.args()``` // Returns a array of the amount of arguments and the actual arguments, eg: `[2, ["slate", "program"]]`
- ```os.mkdir(path)``` // Makes a directory, making any sub-directory's if needed, **(returns true if successful and false if else)** 
- ```os.execute(command)``` // Executes a shell using ```command``` and returns the exit code

**Added in v0.4.0**
- ```os.scale_factor()``` // Returns the os's scale factor (a double) **(Returns 1.0 on failure)**
- ```os.res()``` // Returns a struct with width and height ```resolution{ width, height }``` **(Returns a** ```resolution{ 0, 0 }``` **on failure)**
- ```os.dir_delete(path)``` // Deletes a folder and **all its contents recursively**, returns **true** if successful
- ```os.file_move(old_path, new_path)``` // Renames or moves a file or directory to a new path, returns **true** if successful
- ```os.file_copy(src, dest)``` // Copies a file or folder **recursively**, overwriting if destination exists, returns **true** if successful
- ```os.is_dir(path)``` // Returns **true** if the given path exists and is a **directory**, otherwise false
- ```os.is_file(path)``` // Returns **true** if the given path exists and is a **regular file**, otherwise false
- ```os.cwd()``` // Returns the **current working directory** as a string
- ```os.chdir(path)``` // Changes the **current working directory**, returns **true** if successful
- ```os.path_abs(path)``` // Converts a relative path into a full **absolute path**
- ```os.path_dirname(path)``` // Returns the **parent directory path**, eg: `"a/b/file.txt"` -> `"a/b"`
- ```os.path_filename(path)``` // Returns the **file name portion** of a path, eg: `"a/b/file.txt"` -> `"file.txt"`
- ```os.execute_output(command)``` // Executes a shell command and returns its **captured standard output** as a string
- ```os.setenv(var, val)``` // Sets or updates an **environment variable**, returns **true** if successful
- ```os.cpu_count()``` // Returns the number of **logical CPU cores** available
- ```os.ram()``` // Returns the **total system RAM in KB** (kilobytes), or **-1** on failure
- ```os.ram_free()``` // Returns the **available system RAM in KB** (kilobytes), or **-1** on failure
- ```os.hostname()``` // Returns the computer's **network hostname** as a string
- ```os.username()``` // Returns the **username** of the active OS user account
- ```os.temp_dir()``` // Returns the path to the system **temporary directory**
- ```os.home_dir()``` // Returns the path to the active user's **home directory**
- ```os.pid()``` // Returns the **Process ID (PID)** of the running interpreter program
- ```os.get_clipboard()``` // Returns the current text content of the system **clipboard**, or an empty string if empty or unavailable
- ```os.set_clipboard(text)``` // Sets the system **clipboard text**, returns **true** if successful
- ```os.disk_free(path)``` // Returns available free drive space in bytes, returns **-1** on failure
- ```os.uptime()``` // Returns total system uptime in seconds as a double, returns **-1.0** on failure
- ```os.cpu_usage()``` // Returns overall system **CPU usage percentage** (0.0 to 100.0) calculated between calls
- ```os.is_focused()``` // Returns **true** if the application window currently holds system **focus** **(always returns true for non-windows)** **(Works with the terminal too)**
- ```os.battery()``` // Returns a struct containing system **battery status** with fields `percent` and `charging`, **returns null on non-windows**
- ```os.arch()``` // Returns host CPU architecture (```"x64"```, ```"x86"```, ```"arm64"```, ```"arm"```), returns **"unknown"** if unrecognized
- ```os.env()``` // Returns a struct containing all environment variables
- ```os.file_lwt(path)``` // Returns the last write time in milliseconds (Unix epoch), or -1 if the file is not found
- ```os.script_path``` // Returns the script that is being ran path. **E.g., "C:\Developer\slate\Scripts\script.slate"**

# File #

**Added in v0.4.0**
- ```file.open(path, mode)``` // Opens a file stream with specified mode ("r", "w", "a", "r+") and returns a handle ID **(returns -1 on failure)**
- ```file.read(handle_id, bytes)``` // Reads up to a specified number of bytes from an open file stream and returns a string **(Advances the file stream pointer)**
- ```file.write(handle_id, data)``` // Writes string data to an open file stream and returns the number of bytes written **(-1 on failure)**
- ```file.seek(handle_id, offset, origin)``` // Repositions the file stream pointer (origin: 0 = start, 1 = current, 2 = end) and returns the new position
- ```file.tell(handle_id)``` // Returns the current byte position of the file stream pointer **(-1 on failure)**
- ```file.flush(handle_id)``` // Forces any unwritten changes directly to the file without closing it
- ```file.close(handle_id)``` // Closes an open file stream and releases its system handle
- ```file.eof(handle_id)``` // Returns true if the file stream has reached the end of the file

# Input #

**Added in v0.2.0**

**The strings**
```slate
"a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z",
"0", "1", "2", "3", "4", "5", "6", "7", "8", "9",
"f1", "f2", "f3", "f4", "f5", "f6", "f7", "f8", "f9", "f10", "f11", "f12",
"space", "enter", "escape", "tab", "backspace", "delete", "capslock", "insert", "home", "end", "pageup", "pagedown", "printscreen", "pause",
"shift", "control", "alt", "super", "leftshift", "rightshift", "leftcontrol", "rightcontrol", "leftalt", "rightalt", "left", "right", "up", "down",
"numpad0", "numpad1", "numpad2", "numpad3", "numpad4", "numpad5", "numpad6", "numpad7", "numpad8", "numpad9",
"numpadadd", "numpadsubtract", "numpadmultiply", "numpaddivide", "numpaddecimal", "numpadenter",
"minus", "equals", "leftbracket", "rightbracket", "semicolon", "quote", "comma", "period", "slash", "backslash", "grave"
```
- The three mouse buttons are: `"left"`, `"right"`, `"middle"`
### Functions
- ```input.is_key_down(key)``` // Returns true if the specified keyboard key is currently held down
- ```input.is_mouse_button_down(button)``` // Returns true if the specified mouse button is currently held down
- ```input.mouse_position_x()``` // Returns the current X coordinate of the mouse cursor
- ```input.mouse_position_y()``` // Returns the current Y coordinate of the mouse cursor
- ```input.set_mouse_position(x, y)``` // Sets the mouse cursor to the specified coordinates on the screen
- ```input.drag_mouse(from_x, from_y, to_x, to_y, time, button)``` // Simulates dragging the mouse from one point to another over a specified duration in seconds using the given button to press and release
- ```input.press_mouse(button)``` // Simulates a single click of the mouse button
- ```input.press_key(key)``` // Simulates a single press of the key
- ```input.type_text(text)``` // Simulates typing text from a string
- ```input.key_toggle(key)``` // Creates a watcher for ```key``` and returns a handle to it
- ```input.key_toggle_pressed(handle)``` // Returns true only on the frame ```key``` goes from up to down, otherwise false
- ```input.free_key_toggle(handle)``` // Frees the memory of a key toggle, **```Returns true if successful and false if else```**
- ```input.mouse_toggle(button)``` // Creates an edge-triggered watcher for a mouse ```button``` and returns a handle to it
- ```input.mouse_toggle_pressed(handle)``` // Returns true only on the frame ```button``` goes from up to down, otherwise false, call once per loop/coroutine resume
- ```input.free_mouse_toggle(handle)``` // Frees the memory of a mouse toggle, **```Returns true if successful and false if else```**

**Added in v0.4.0**
- ```input.mouse_scroll(amount)``` // Scrolls the mouse wheel vertically (positive for up, negative for down)
- ```input.move_mouse_by(dx, dy)``` // Moves the cursor by a relative offset from its current position
- ```input.key_down(key)``` // Presses a key down without releasing it
- ```input.key_up(key)``` // Releases a previously pressed key
- ```input.mouse_down(button)``` // Presses a mouse button down without releasing it
- ```input.mouse_up(button)``` // Releases a previously pressed mouse button
- ```input.wait_for_key(key)``` // Blocks execution until the specified key is pressed down
- ```input.jittered_delay(base_micros, jitter_percent)``` // Waits for a specified duration randomized by a jitter percentage
- ```input.get_down_keys()``` // Returns an array of strings representing all keys currently held down
- ```input.repeat_key_press(key, count, delay_ms)``` // Presses and releases a key multiple times, optionally spaced out by a delay in milliseconds
- ```input.key_combo_press(combo_array)``` // Presses every key in the array down in order, then releases them in reverse order

# Data #
- ```data.save_manager("app_name", backup_amount, overwrite)``` // Makes a SaveManager class, keep overwrite false most of the time
- ```data.map()``` // Makes a data map
- ```data.write(map, "key", value)``` // Writes a value to a map
- ```data.read(map, "key", default_value)``` // Reads a value from a map, The type of the *```default_value```* determines what type is returned. Returns *```default_value```* if the key or map is not found
- ```data.save(map, SaveManager, save_file_number)``` // Saves a map to **disk in appdata** **(or the linux/macos equivalent)** with the **SaveManager's appname** with a **save file number**, **```Returns true if successful and false if else```**, will load backups if the main file fails to save
- ```data.load(SaveManager, save_file_number)``` // Returns a map from the *```save file number```*
- ```data.delete(SaveManager, save_file_number)``` // Deletes a specific save file by its *```save file number```*, **```Returns true if successful and false if else```**
- ```data.delete_all(SaveManager)``` // Deletes all save files managed by the SaveManager, **```Returns true if successful and false if else```**
- ```data.free_map(map)``` // Frees the memory of a data map, **```Returns true if successful and false if else```**
- ```data.free_save_manager(SaveManager)``` // Frees the memory of a SaveManager, **```Returns true if successful and false if else```**
- Example using some of these:
```slate
var SaveManager = data.save_manager("App", 3, false);
var map = data.Map(); 
data.write(map, "hp", 1000);
var random_save_num = math.random_int(1, 3);
data.save(map, SaveManager, random_save_num);

var map2 = data.load(SaveManager, 1);
print(data.read(map2, "hp", random_save_num));
```

# String #
- ```string.charCode(string, index)``` // Returns the ASCII value of the character at the index, Runtime error if out of bounds
- ```string.sub(string, start, end)``` // Returns a substring from the start index to the end index, auto clamps index and **supports negative indexing**, ```-1 is the last character, -2 is the second to last, etc```. **(Is inclusive (string.length - 1 for getting the last index is correct, not string.length))**
- ```string.lower(string)``` // Returns a new string with all characters converted to lowercase
- ```string.upper(string)``` // Returns a new string with all characters converted to uppercase
- ```string.reverse(string)``` // Returns a reversed copy of the string
- ```string.rep(string, repeat_count)``` // Returns a string that repeats the input string a number of times
- ```string.hash(string)``` // Returns a **positive 64-bit hash integer** of a string using SipHash
- ```string.fasthash(string)``` // Returns a **positive 64-bit hash integer** of a string using Wyhash

**Added in v0.2.0**
- ```string.split(string, delimiter)``` // Splits ```string``` on every occurrence of ```delimiter``` and returns an **array of strings**. An empty ```delimiter``` splits into individual characters
- ```string.trim(string)``` // Returns a new string with leading and trailing whitespace removed
- ```string.contains(string, substring)``` // Returns true if ```substring``` occurs anywhere in ```string```, otherwise false
- ```string.find(string, substring)``` // Returns the **index of the first occurrence** of ```substring``` in ```string```, or -1 if not found
- ```string.replace(string, old, new)``` // Returns a new string with **every occurrence** of ```old``` replaced with ```new```
- ```string.join(array, delimiter)``` // Joins every element of ```array``` into a single string, separated by ```delimiter```
- ```string.starts_with(string, prefix)``` // Returns true if ```string``` begins with ```prefix```, otherwise false
- ```string.ends_with(string, suffix)``` // Returns true if ```string``` ends with ```suffix```, otherwise false
- ```string.count(string, substring)``` // Returns the **number of non-overlapping occurrences** of ```substring``` in ```string```
- ```string.pad_left(string, length, pad_char)``` // Pads ```string``` on the left with ```pad_char``` until it reaches ```length```, returns ```string``` unchanged if it's already that long or longer
- ```string.pad_right(string, length, pad_char)``` // Pads ```string``` on the right with ```pad_char``` until it reaches ```length```, returns ```string``` unchanged if it's already that long or longer

**Added in v0.3.0**
- ```string.char(character_code)``` // Returns the character from a character code, the inverse of string.charCode

**Added in v0.4.0**
- ```string.regex(string, pattern)``` // Returns true if the regular expression pattern matches the string exactly, or throws an error if the pattern syntax is invald **(uses std::regex)**
- ```string.rfind(string, substring)``` // Returns the **index of the last occurrence** of ```substring``` in ```string```, or -1 if not found
- ```string.capitalize(string)``` // Returns a new string with the **first character converted to uppercase** and the remaining characters left unchanged
- ```string.trim_left(string)``` // Returns a new string with **leading whitespace** removed
- ```string.trim_right(string)``` // Returns a new string with **trailing whitespace** removed
- ```string.is_digit(string)``` // Returns true if the string is non-empty and **consists entirely of numeric digits** (0-9), otherwise false
- ```string.center(string, length, pad_char)``` // Centers the string within a given length by **padding both sides** evenly with ```pad_char```

# Array #
 
**Added in v0.2.0**
- ```array.contains(array, value)``` // Returns true if ```value``` is found anywhere in ```array```, otherwise false
- ```array.index_of(array, value)``` // Returns the **index of the first occurrence** of ```value``` in ```array```, or -1 if not found
- ```array.sort(array)``` // Sorts ```array``` **in place** in ascending order **(numbers and strings only)**, **```Returns true if successful and false if else```**
- ```array.sort_by(array, comparator)``` // Sorts ```array``` **in place** using ```comparator(a, b)```, a function returning true if ```a``` should come before ```b```, **```Returns true if successful and false if else```**
- ```array.reverse(array)``` // Reverses ```array``` **in place**, **```Returns true if successful and false if else```**
- ```array.slice(array, start, end)``` // Returns a **new array** containing the elements from the start index to the end index, auto clamps index and **supports negative indexing**, ```-1 is the last element, -2 is the second to last, etc```
- ```array.concat(array1, array2)``` // Returns a **new array** containing every element of ```array1``` followed by every element of ```array2```

**Added in v0.3.0**
- ```array.find(array, predicate)``` // Returns the index of the first element in array that matches `predicate(value)` (`predicate(value)` needs to return a boolean), **```returns -1 if none found```**

# Memory #

**Added in v0.3.0**
- ```memory.move(&var)``` // Steals the value from ```var``` and returns it, setting ```var``` to null (std::move)
- ```memory.swap(&a, &b)``` // Swaps the values of variables ```a``` and ```b``` in-place
- ```memory.pool_create(factory_fn, initial_capacity, max_capacity)``` // Creates a new ```object pool handle``` using a ```factory function```, ```initial capacity```, and ```maximum capacity``` **(```-1``` for unlimited)**
- ```memory.pool_take(pool_id)``` // Retrieves an available object from the ```pool``` **(or constructs a new one if empty)**
- ```memory.pool_release(pool_id, item)``` // Recycles ```item``` back into the ```pool```
- ```memory.pool_size(pool_id)``` // Returns an array ```[available_count, in_use_count]``` for the specified pool
- ```memory.pool_destroy(pool_id)``` // Deletes a object pool

# json #

**Added in v0.4.0**
- `json.stringify(value)` // Serializes a value to a JSON string.
- `json.parse(string)` // Parses a JSON string into a struct, array, or primitive. Returns `null` if malformed.
- `json.is_valid(string)` // Returns `true` if the string is valid JSON without instantiating objects.

# Net #

**Added in v0.4.0**
- `net.poll()` // Drives the network event loop. Returns the number of executed event handlers.
- `net.has_pending()` // Returns true if there are active or pending asynchronous operations queued in the event loop.
- `net.resolve(host)` // Synchronously resolves a hostname to an IP address string.
- `net.async_resolve(host, callback)` // Asynchronously resolves a host. `callback(ip_string)` is executed upon completion.
- `net.get_local_ip()` // Returns the primary local IPv4 address of the current device.
- `net.parse_url(url)` // Parses a URL string into a struct containing `.scheme`, `.host`, `.port`, and `.path`.
- `net.is_ip_valid(ip_str)` // Validates whether a string is a valid IPv4 or IPv6 address.
- `net.ping(host, timeout_ms)` // Performs a connection test against a host on port 80. Returns true if reachable within `timeout_ms`.

### tcp:
- `net.tcp.connect(host, port)` // Synchronously connects to a TCP endpoint in blocking mode. Returns a socket handle (long) or 0 on failure. `port` is a string.
- `net.tcp.connect_nonblocking(host, port)` // Connects to a TCP endpoint and sets the socket to non-blocking mode. Returns socket handle or 0. `port` is a string.
- `net.tcp.async_connect(host, port, callback)` // Asynchronously connects to a TCP endpoint. `callback(sock_handle)` is executed with the socket handle or 0 on error. `port` is a string.
- `net.tcp.send(sock_handle, data)` // Synchronously sends a string over a TCP socket. Returns true on success.
- `net.tcp.recv(sock_handle, max_bytes)` // Synchronously receives up to `max_bytes` from a TCP socket. Returns the received string. Blocks until data arrives or error occurs.
- `net.tcp.recv_exact(sock_handle, num_bytes)` // Synchronously blocks until exactly `num_bytes` are read from the socket. Returns the received string.
- `net.tcp.async_send(sock_handle, data, callback)` // Asynchronously writes data to a TCP socket. `callback(success_bool)` is executed upon completion.
- `net.tcp.async_recv(sock_handle, max_bytes, callback)` // Asynchronously reads up to `max_bytes`. `callback(data_string)` is executed when data arrives. Returns empty string on error or if no data.
- `net.tcp.listen(port)` // Binds and listens for incoming TCP connections on `port`. Returns an acceptor handle (long) or 0. `port` is a long.
- `net.tcp.accept(acceptor_handle)` // Synchronously accepts a pending client connection. Returns client socket handle or 0.
- `net.tcp.async_accept(acceptor_handle, callback)` // Asynchronously waits for a client connection. `callback(client_sock_handle)` is invoked on accept. Passes 0 on error.
- `net.tcp.stop_listen(acceptor_handle)` // Closes the TCP listener/acceptor handle. Returns true on success.
- `net.tcp.close(sock_handle)` // Gracefully shuts down and frees the TCP socket handle. Returns true on success.
- `net.tcp.shutdown(sock_handle, mode)` // Shuts down socket communication channels. `mode` can be `"send"`, `"receive"`, or `"both"`. Returns true on success.
- `net.tcp.set_blocking(sock_handle, blocking)` // Toggles blocking mode on a socket (`true` for blocking, `false` for non-blocking). Returns true on success.
- `net.tcp.set_timeout(sock_handle, timeout_ms)` // Configures read/write timeout in milliseconds for socket operations. Returns true on success.
- `net.tcp.set_keepalive(sock_handle, enable)` // Enables or disables TCP keep-alive on the socket. Returns true on success.
- `net.tcp.set_nodelay(sock_handle, enable)` // Enables or disables TCP_NODELAY (Nagle's algorithm) on the socket. Returns true on success.
- `net.tcp.set_reuse_address(acceptor_handle, enable)` // Enables or disables address reuse (`SO_REUSEADDR`) on an acceptor handle. Returns true on success.
- `net.tcp.bytes_available(sock_handle)` // Returns the number of bytes currently available to read without blocking. Returns 0 if no data or error.
- `net.tcp.is_open(sock_handle)` // Returns true if the socket handle is valid and active.
- `net.tcp.get_local_info(sock_or_acceptor_handle)` // Returns a struct with `.address` and `.port` for local endpoint. Works for both sockets and acceptors.
- `net.tcp.get_peer_info(sock_handle)` // Returns a struct with `.address` and `.port` for remote peer endpoint.

### ssl:
- `net.ssl.connect(host, port)` // Synchronously establishes a raw SSL/TLS TCP stream to a remote host. Returns an SSL socket handle (long) or 0 on failure. `port` is a string.
- `net.ssl.async_connect(host, port, callback)` // Asynchronously establishes an SSL/TLS stream. `callback(ssl_handle)` is executed with the handle or 0 on error. `port` is a string.
- `net.ssl.send(ssl_handle, data)` // Synchronously writes data over an encrypted SSL stream. Returns true on success.
- `net.ssl.async_send(ssl_handle, data, callback)` // Asynchronously writes data over SSL. `callback(success_bool)` is executed upon completion.
- `net.ssl.recv(ssl_handle, max_bytes)` // Synchronously receives up to `max_bytes` over an SSL stream. Returns the decrypted string. Blocks until data arrives or error occurs.
- `net.ssl.async_recv(ssl_handle, max_bytes, callback)` // Asynchronously reads up to `max_bytes` over SSL. `callback(data_string)` is executed when data arrives. Returns empty string on error or no data.
- `net.ssl.set_verify(ssl_handle, verify)` // Enables or disables SSL/TLS peer certificate verification. Returns true on success.
- `net.ssl.close(ssl_handle)` // Gracefully shuts down and frees an SSL socket handle. Returns true on success.

### http:
- `net.http.get(host, port, target)` // Synchronously performs an HTTP/HTTPS GET request and returns the raw response body string. Returns empty string on failure. `port` is a string.
- `net.http.request(method, host, port, target, body)` // Synchronously executes an HTTP/HTTPS request with a specified method and body string. Returns response body string. Returns empty string on failure. `port` is a string.
- `net.http.request_full(method, host, port, target, body, headers)` // Synchronously performs an HTTP/HTTPS request with a custom header struct. Returns a struct with `.status` and `.body`. `.status = 0` and `.body = ""` on failure. `port` is a string.
- `net.http.async_get(host, port, target, callback)` // Asynchronously executes an HTTP/HTTPS GET request. `callback(body_string)` receives response body. Returns empty string on failure. `port` is a string.
- `net.http.async_request(method, host, port, target, body, headers, callback)` // Asynchronously executes an HTTP/HTTPS request. `callback(res_struct)` receives response struct containing `.status`, `.body`, and `.success`. `port` is a string.
- `net.http.listen(port)` // Binds an HTTP server to `port`. Returns an acceptor handle (long) or 0 on failure. `port` is a long.
- `net.http.accept(acceptor_handle)` // Synchronously accepts a pending HTTP request. Returns a struct containing `.handle`, `.method`, `.target`, `.body`, and `.headers`.
- `net.http.async_accept(acceptor_handle, callback)` // Asynchronously waits for an HTTP request. `callback(req_handle, req_struct)` is executed upon receipt. `req_struct` contains `.method`, `.target`, `.body`, and `.headers`.
- `net.http.respond(req_handle, status_code, body, headers)` // Sends an HTTP response and closes the connection. `headers` is a struct (optional). Returns true on success.
- `net.http.respond_custom(req_handle, status_code, body, content_type, headers)` // Sends an HTTP response with status code, custom content type, and headers struct. Returns true on success.
- `net.http.respond_file(req_handle, status_code, file_path, content_type)` // Zero-copy streams a static file directly from disk to the HTTP client. Returns true on success.
- `net.http.redirect(req_handle, location_url, status_code)` // Sends an HTTP redirect response (e.g., status 301 or 302). Returns true on success.
- `net.http.parse_query(target_url)` // Parses URL query parameters (`?key=val`) into a key-value struct.
- `net.http.is_websocket(req_handle)` // Returns true if an incoming HTTP request contains a WebSocket upgrade header.
- `net.http.upgrade_websocket(req_handle)` // Performs the HTTP-to-WebSocket handshake and returns a WebSocket handle (long).
- `net.http.close(req_handle)` // Aborts and frees an HTTP request context without sending a response. Returns true on success.
- `net.http.stop_listen(acceptor_handle)` // Closes the HTTP server acceptor handle. Returns true on success.
- `net.http.url_encode(value)` // Returns a percent-encoded string formatted for URLs.
- `net.http.url_decode(value)` // Decodes a percent-encoded URL string back to plain text.

### ws:
- `net.ws.connect(host, port, target)` // Connects to a WebSocket endpoint over WS or WSS. Returns a WebSocket handle (long) or 0 on failure. `port` is a string.
- `net.ws.async_connect(host, port, target, callback)` // Asynchronously establishes a WS or WSS connection. `callback(ws_handle, success_bool)` is executed. `port` is a string.
- `net.ws.send(ws_handle, message)` // Synchronously sends a text frame over an open WebSocket connection. Returns true on success.
- `net.ws.send_binary(ws_handle, binary_data)` // Sends a binary frame over an open WebSocket connection. Returns true on success.
- `net.ws.async_send(ws_handle, message, callback)` // Asynchronously sends a text frame. `callback(success_bool)` is executed upon completion.
- `net.ws.async_send_binary(ws_handle, binary_data, callback)` // Asynchronously sends a binary frame. `callback(success_bool)` is executed upon completion.
- `net.ws.recv(ws_handle)` // Synchronously receives the next message frame from a WebSocket connection. Returns frame string. Blocks until message arrives.
- `net.ws.async_recv(ws_handle, callback)` // Asynchronously receives the next message frame. `callback(data_string)` is executed when data arrives. Returns empty string on error or closure.
- `net.ws.ping(ws_handle, payload)` // Sends a custom WebSocket ping frame with an optional payload string for keep-alives. Returns true on success.
- `net.ws.is_open(ws_handle)` // Returns true if the WebSocket connection is still open and active.
- `net.ws.close(ws_handle)` // Closes the WebSocket session and frees the handle. Returns true on success. **(Never close inside a async callback)**

### udp:
- `net.udp.bind(port)` // Binds a UDP socket to a local port. Returns UDP socket handle (long) or 0. `port` is a long.
- `net.udp.send(host, port, data)` // Sends a raw UDP packet to a host and port. Returns true on success. `port` is a string.
- `net.udp.recv(socket_handle, max_bytes)` // Synchronously receives up to `max_bytes` from a UDP socket. Returns packet string. Blocks until data arrives.
- `net.udp.recv_from(socket_handle, max_bytes)` // Synchronously receives a UDP packet. Returns struct with `.data`, `.address`, and `.port`. Blocks until data arrives.
- `net.udp.async_send(socket_handle, host, port, data, callback)` // Asynchronously sends a UDP packet. `callback(success_bool)` is executed on completion. `port` is a string.
- `net.udp.async_recv_from(socket_handle, max_bytes, callback)` // Asynchronously waits for a packet. `callback(res_struct)` receives struct with `.data`, `.address`, and `.port`.
- `net.udp.set_broadcast(socket_handle, enable)` // Enables or disables packet broadcasting (`SO_BROADCAST`) on a UDP socket. Returns true on success.
- `net.udp.set_ttl(socket_handle, ttl)` // Sets the Time-To-Live (TTL) value for UDP packets. Returns true on success.
- `net.udp.join_multicast_group(socket_handle, multicast_addr)` // Joins a UDP multicast group for receiving multicast traffic. Returns true on success.
- `net.udp.leave_multicast_group(socket_handle, multicast_addr)` // Leaves a UDP multicast group. Returns true on success.
- `net.udp.close(socket_handle)` // Closes and frees a UDP socket handle. Returns true on success.

# Console #

>std::cout and std::cerr

**Added in v0.3.0**
- ```console.out(message)``` // Prints a message to standard output using the active color state
- ```console.fout(message)``` // Prints a message to standard error (stderr) using the active error color state
- ```console.width()``` // Returns the consoles width
- ```console.height()``` // Returns the consoles height
- ```console.color(r, g, b)``` // Sets the persistent RGB text color for standard output
- ```console.fcolor(r, g, b)``` // Sets the persistent RGB text color for standard error (stderr)
- ```console.reset()``` // Resets all terminal colors and text formatting back to default
- ```console.flush()``` // Flushes the standard output stream buffer immediately
- ```console.fflush()``` // Flushes the standard error stream buffer immediately
- ```console.clear()``` // Clears the entire terminal screen and resets the cursor to position (1, 1)
- ```console.clear_line()``` // Clears the current terminal line from the cursor onwards and returns the cursor to the start
- ```console.clear_up()``` // Clears the screen from the current cursor position up to the top
- ```console.clear_down()``` // Clears the screen from the current cursor position down to the bottom
- ```console.command(cmd)``` // Sends a raw string or ANSI command directly to standard output and flushes
- ```console.read_key()``` // Returns a string of whatever key was pressed, raw mode must be enabled or you will have to wait for the enter key, all things are: ```["a", "A", "b", "B", "c", "C", "d", "D", "e", "E", "f", "F", "g", "G", "h", "H", "i", "I", "j", "J", "k", "K", "l", "L", "m", "M", "n", "N", "o", "O", "p", "P", "q", "Q", "r", "R", "s", "S", "t", "T", "u", "U", "v", "V", "w", "W", "x", "X", "y", "Y", "z", "Z", "0", "1", "2", "3", "4", "5", "6", "7", "8", "9", " ", "!", "\"", "#", "$", "%", "&", "'", "(", ")", "*", "+", ",", "-", ".", "/", ":", ";", "<", "=", ">", "?", "@", "[", "\\", "]", "^", "_", "`", "{", "|", "}", "~", "enter", "backspace", "space", "escape", "tab", "up", "down", "left", "right", "home", "end", "delete", "f1", "f2", "f3", "f4", "f5", "f6", "f7", "f8", "f9", "f10", "f11", "f12", "ctrl+a", "ctrl+b", "ctrl+c", "ctrl+d", "ctrl+e", "ctrl+f", "ctrl+g", "ctrl+h", "ctrl+i", "ctrl+j", "ctrl+k", "ctrl+l", "ctrl+m", "ctrl+n", "ctrl+o", "ctrl+p", "ctrl+q", "ctrl+r", "ctrl+s", "ctrl+t", "ctrl+u", "ctrl+v", "ctrl+w", "ctrl+x", "ctrl+y", "ctrl+z", "alt+a", "alt+b", "alt+c", "alt+d", "alt+e", "alt+f", "alt+g", "alt+h", "alt+i", "alt+j", "alt+k", "alt+l", "alt+m", "alt+n", "alt+o", "alt+p", "alt+q", "alt+r", "alt+s", "alt+t", "alt+u", "alt+v", "alt+w", "alt+x", "alt+y", "alt+z", "ctrl+up", "ctrl+down", "ctrl+left", "ctrl+right", "alt+up", "alt+down", "alt+left", "alt+right"]```
- ```console.has_input()``` // Returns true if the console has any input (use for non-blocking key reading)
- ```console.raw_mode(enable)``` // Enables or disables terminal raw mode for instant key interception
- ```console.cursor.set_pos(x, y)``` // Moves the cursor to the specified absolute X and Y coordinates (1-based indexing)
- ```console.cursor.get_pos()``` // Queries the terminal and returns the current cursor position as an array [x, y]
- ```console.cursor.show()``` // Makes the blinking terminal cursor visible
- ```console.cursor.hide()``` // Hides the blinking terminal cursor
- ```console.cursor.up(n)``` // Moves the cursor up by n rows relative to its current position
- ```console.cursor.down(n)``` // Moves the cursor down by n rows relative to its current position
- ```console.cursor.left(n)``` // Moves the cursor left by n columns relative to its current position
- ```console.cursor.right(n)``` // Moves the cursor right by n columns relative to its current position
- ```console.cursor.save()``` // Saves the current cursor position in terminal memory
- ```console.cursor.restore()``` // Restores the cursor position back to the last saved location
- ```console.style.bold(enable)``` // Enables or disables bold text formatting
- ```console.style.dim(enable)``` // Enables or disables faint/dim text formatting
- ```console.style.italic(enable)``` // Enables or disables italic text formatting
- ```console.style.underline(enable)``` // Enables or disables underlined text formatting
- ```console.style.blink(enable)``` // Enables or disables blinking text
- ```console.style.reverse(enable)``` // Reverses foreground and background colors
- ```console.bg(r, g, b)``` // Sets the persistent RGB background color for standard output
- ```console.fbg(r, g, b)``` // Sets the persistent RGB background color for standard error (stderr)

# Image #

>stb_image and stb_image_write, everything is mutlithreaded except for scriptable things **(image.transform, etc is single threaded)**

**Added in v0.3.0**

*Supported formats:*
- **PNG** (`.png`)
- **JPEG** (`.jpg`, `.jpeg`)
- **BMP** (`.bmp`)
- **TGA** (`.tga`)
- **PSD** (`.psd`)
- **HDR** (`.hdr`)
- **PIC** (`.pic`)
- **GIF** (`.gif` -> first frame)

*Functions:*
- ```image.load(path)``` // Loads an image file from disk and returns a handle to it. **```Returns -1 on failure```**
- ```image.new(w, h)``` // Creates a blank RGBA image buffer with dimensions `w`x`h` and returns a handle. **```Returns -1 if dimensions are invalid```**
- ```image.dimensions(handle)``` // Returns an **array of integers** `[width, height]`. **```Returns [0, 0] if handle is invalid```**
- ```image.save(handle, path)``` // Writes the image buffer to disk at `path`. **```Returns true on success, false if else```**
- ```image.free(handle)``` // Frees the memory of the image buffer associated with `handle`
- ```image.clone(handle)``` // Duplicates the image buffer and returns a handle to the new copy. **```Returns -1 on failure```**
- ```image.valid(handle)``` // Returns `true` if the image handle exists, `false` otherwise.
- ```image.get_pixel(handle, x, y)``` // Returns an **array of RGBA values** `[r, g, b, a]` at `(x, y)`. **```Returns [0, 0, 0, 0] if out of bounds or invalid handle```**
- ```image.set_pixel(handle, x, y, r, g, b, a)``` // Sets the RGBA color at `(x, y)`. Color values are clamped automatically between 0 and 255
- ```image.get_pixels(handle, x, y, width, height)``` // Retrieves a 2D array of RGBA color arrays inside `(x, y, width, height)`. **`Returns array of RGBA color arrays (out-of-bounds pixels return null)`**
- ```image.set_pixels(handle, x, y, width, height, r, g, b, a)``` // Fills all pixels within `(x, y, width, height)` with the provided RGBA values. Clamped between 0 and 255.
- ```image.draw(src_handle, dst_handle, dst_x, dst_y)``` // Blits (draws) the source buffer onto the destination buffer at `(dst_x, dst_y)` using alpha compositing.
- ```image.transform(handle, callback)``` // Iterates over every pixel using a script callback `(x, y, r, g, b, a) -> [r, g, b, a]`. **`Returns new image handle, or -1 on failure`**.

*Eg:*
```rust
var new_img = image.transform(img, fn(x, y, r, g, b, a) {
    return [b, g, r, a]; // Swaps R and B
});
```
- ```image.crop(handle, x, y, w, h)``` // Crops a region starting at `(x, y)` with size `w`x`h`. **`Returns new image handle, or -1 on failure`**
- ```image.resize(handle, new_w, new_h)``` // Rescales an image buffer using multithreaded **bilinear interpolation**. **```Returns new image handle, or -1 on failure```**
- ```image.fast_resize(handle, new_w, new_h)``` // Rescales an image buffer using **nearest-neighbor sampling** (ideal for pixel art). **```Returns new image handle, or -1 on failure```**
- ```image.rotate(handle, degrees)``` // Rotates an image by degrees, recalculating dimensions to prevent clipping. **`Returns new image handle, or -1 on failure`**
- ```image.grayscale(handle)``` // Converts image to grayscale. **`Returns new image handle, or -1 on failure`**
- ```image.invert(handle)``` // Inverts RGB color channels. **`Returns new image handle, or -1 on failure`**
- ```image.adjust_brightness(handle, factor)``` // Scales RGB channels by multiplier `factor`. **`Returns new image handle, or -1 on failure`**
- ```image.blur(handle, radius)``` // Applies a box blur with window radius `radius`. **`Returns new image handle, or -1 on failure`**

**In place (modifies the image directly)**
- ```image.grayscale_self(handle)``` // Converts image to grayscale in-place. **`Returns true on success, false if else`**
- ```image.invert_self(handle)``` // Inverts RGB color channels in-place. **`Returns true on success, false if else`**
- ```image.adjust_brightness_self(handle, factor)``` // Scales RGB channels by multiplier `factor` in-place. **`Returns true on success, false if else`**
- ```image.blur_self(handle, radius)``` // Applies an $\mathcal{O}(1)$ sliding-window box blur in-place. **`Returns true on success, false if else`**
- ```image.gaussian_blur_self(handle, sigma)``` // Applies a 3-pass $\mathcal{O}(1)$ sliding-window Gaussian blur with standard deviation `sigma` in-place. *(Is about 97% accurate to real gaussian blur and is about 4x faster on average)* **`Returns true on success, false if else`**

**Example:**
```slate
// Create a 100x100 canvas
var img = image.new(100, 100);

var dimensions = image.dimensions(img);
// Generate the gradient
var gradient_img = image.transform(img, fn(x, y, r, g, b, a) {
    var new_r = (x * 255) / dimensions[0];
    var new_g = (y * 255) / dimensions[1];
    return [new_r, new_g, 150, 255];
});

image.save(gradient_img, "output.png");

// Free all buffers
image.free(img);
image.free(gradient_img);
```

# Audio #

>miniaudio

**Added in v0.3.0**

- ```audio.load(path)``` // Loads an audio file from disk and returns a handle to it. **```Returns -1 on failure```**
- ```audio.play(handle)``` // Starts or resumes playback of the audio associated with ```handle```
- ```audio.pause(handle)``` // Pauses playback of the audio associated with ```handle```
- ```audio.stop(handle)``` // Stops playback and seeks the audio back to the beginning
- ```audio.clone(handle)``` // Duplicates an existing audio source handle into a independent playback instance (ideal for sound effect pooling). Shares underlying sound decoder memory. **`Returns new audio handle, or -1 on failure`**
- ```audio.pause_all()``` // Pauses playback for all currently active audio handles across the engine.
- ```audio.resume_all()``` // Resumes playback for all paused audio handles across the engine.
- ```audio.is_playing(handle)``` // Returns true if the audio source is currently playing, otherwise false
- ```audio.length(handle)``` // Returns the total length of the audio file in seconds as a float
- ```audio.get_position(handle)``` // Returns the current playback position in seconds as a float
- ```audio.set_position(handle, seconds)``` // Seeks playback to the specified time in seconds
- ```audio.set_volume(handle, volume)``` // Sets the volume level for the audio source (e.g. `1.0` for 100%, `0.5` for 50%)
- ```audio.set_pitch(handle, pitch)``` // Sets playback pitch/speed multiplier (`1.0` is default, `0.5` is half-speed/octave down, `2.0` is double-speed/octave up)
- ```audio.set_pan(handle, pan)``` // Sets the stereo panning (`-1.0` for full left, `0.0` for center, `1.0` for full right)
- ```audio.set_looping(handle, loop)``` // Enables or disables automatic looping for the audio source (`true` or `false`)
- ```audio.set_master_volume(volume)``` // Sets the global master volume across all audio sources (`1.0` for 100%, `0.0` for mute)
- ```audio.free(handle)``` // Uninitializes the audio source and frees memory associated with ```handle```
- ```audio.shutdown()``` // Frees all active audio instances and cleans up the global audio engine

**Added in v0.4.0**
- ```audio.get_volume(handle)``` // Returns the current volume level of the audio source as a float (`0.0` to `1.0`). **`Returns 0.0 if invalid handle`**
- ```audio.get_pitch(handle)``` // Returns the current pitch/speed multiplier as a float. **`Returns 1.0 if invalid handle`**
- ```audio.get_pan(handle)``` // Returns the current stereo panning value as a float (`-1.0` to `1.0`). **`Returns 0.0 if invalid handle`**
- ```audio.get_looping(handle)``` // Returns `true` if automatic looping is enabled for the audio source, `false` otherwise.
- ```audio.get_master_volume()``` // Returns the global master volume level across all audio sources as a float (`0.0` to `1.0`).
- ```audio.fade(handle, volume_start, volume_end, duration_seconds)``` // Smoothly fades the volume from `volume_start` to `volume_end` over `duration_seconds`.
- ```audio.fade_out_at(handle, start_seconds, duration_seconds)``` // Schedules a fade-out to `0.0` volume starting at timestamp `start_seconds` over `duration_seconds`.

**Example:**

```slate
// Set global master volume to 90%
audio.set_master_volume(0.9);

// Load an audio file
var bgm = audio.load("music.mp3");

if (bgm != -1) {
    // Set looping, 80% volume, normal pitch, and centered stereo panning
    audio.set_looping(bgm, true);
    audio.set_volume(bgm, 0.8);
    audio.set_pitch(bgm, 1.0);
    audio.set_pan(bgm, 0.0);

    // Get total duration of the track
    var total_time = audio.length(bgm);
    print("Track length: " + total_time + " seconds");

    // Seek directly to 15 seconds in
    audio.set_position(bgm, 15.0);

    // Play the audio
    audio.play(bgm);

    // Check playback status and query current position, activates after the stop since audio is on a different thread
    if (audio.is_playing(bgm)) {
        var current_pos = audio.get_position(bgm);
        print("Playing background music at: " + current_pos + "s");
    }
    //Waiting until the sound finishes and letting it loop once
    os.sleep(total_time * 2);

    // Stop and free resource when done
    audio.stop(bgm);
    audio.free(bgm);
}

// Clean up the global audio on exit
audio.shutdown();
```

# Color #

> Color processing

**Added in v0.3.0**

*Color Representation:* `[r, g, b, a]`

*Functions:*
- ```color.WHITE()``` // Returns RGBA array `[255, 255, 255, 255]`
- ```color.BLACK()``` // Returns RGBA array `[0, 0, 0, 255]`
- ```color.RED()``` // Returns RGBA array `[255, 0, 0, 255]`
- ```color.GREEN()``` // Returns RGBA array `[0, 255, 0, 255]`
- ```color.BLUE()``` // Returns RGBA array `[0, 0, 255, 255]`
- ```color.YELLOW()``` // Returns RGBA array `[255, 255, 0, 255]`
- ```color.MAGENTA()``` // Returns RGBA array `[255, 0, 255, 255]`
- ```color.CYAN()``` // Returns RGBA array `[0, 255, 255, 255]`
- ```color.CLEAR()``` // Returns RGBA array `[0, 0, 0, 0]`
- ```color.rgb(r, g, b)``` // Creates a color array with an alpha value of 255. **```Returns [r, g, b, 255]```**
- ```color.rgba(r, g, b, a)``` // Creates a full RGBA color array. **```Returns [r, g, b, a]```**
- ```color.rgbf(r, g, b)``` // Accepts normalized floating-point channels (0.0 - 1.0) and converts them to RGBA. **```Returns [r, g, b, 255]```**
- ```color.hex(hex_str)``` // Parses a hex string (`"#RRGGBB"` or `"RRGGBB"`). **```Returns [r, g, b, 255]```**
- ```color.hsva(h, s, v, a)``` // Converts Hue (0-360), Saturation (0.0-1.0), Value (0.0-1.0), and Alpha (0.0-1.0) into an RGBA array. **```Returns [r, g, b, a]```**
- ```color.to_hex(color_arr)``` // Converts an RGBA color array into a hex string. **```Returns "#RRGGBB"```**
- ```color.to_hexa(color_arr)``` // Converts an RGBA color array into a hex string with alpha. **```Returns "#RRGGBBAA"```**
- ```color.to_hsv(color_arr)``` // Converts an RGBA color array into HSV representation. **```Returns [h, s, v]```**
- ```color.lerp(c1, c2, t)``` // Linearly interpolates between two color arrays by factor `t` (0.0 to 1.0). **```Returns new RGBA array```**
- ```color.blend(src, dst)``` // Alpha-blends the `src` color over the `dst` background color. **```Returns new RGBA array```**
- ```color.luminance(color_arr)``` // Calculates perceived relative luminance. **```Returns float between 0.0 and 1.0```**
- ```color.invert(color_arr)``` // Inverts RGB values while preserving alpha. **```Returns new RGBA array```**
- ```color.grayscale(color_arr)``` // Converts the color to its perceived grayscale equivalent. **```Returns new RGBA array```**
- ```color.lighten(color_arr, amount)``` // Increases HSV Value brightness by `amount` (0.0 to 1.0). **```Returns new RGBA array```**
- ```color.darken(color_arr, amount)``` // Decreases HSV Value brightness by `amount` (0.0 to 1.0). **```Returns new RGBA array```**
- ```color.saturate(color_arr, amount)``` // Increases HSV Saturation by `amount` (0.0 to 1.0). **```Returns new RGBA array```**
- ```color.desaturate(color_arr, amount)``` // Decreases HSV Saturation by `amount` (0.0 to 1.0). **```Returns new RGBA array```**
- ```color.distance(c1, c2)``` // Calculates Euclidean distance between two colors in 3D RGB space. **```Returns float```**

**Example:**
```slate
// 1. Preset Getters
var w = color.WHITE();
var k = color.BLACK();
var r = color.RED();
var g = color.GREEN();
var b = color.BLUE();
var y = color.YELLOW();
var m = color.MAGENTA();
var c = color.CYAN();
var clr = color.CLEAR();

// 2. Constructors
var c_rgb  = color.rgb(255, 128, 0);
var c_rgba = color.rgba(255, 0, 128, 200);
var c_rgbf = color.rgbf(0.2, 0.4, 0.8);
var c_hex  = color.hex("#3B82F6");
var c_hsva = color.hsva(180.0, 1.0, 0.8, 1.0);

// 3. Formatters and versions
print("Hex: " + color.to_hex(c_hex));
print("HexA: " + color.to_hexa(c_rgba));
var hsv = color.to_hsv(c_hsva);
print("HSV Hue: " + hsv.at(0));

// 4. Blending and Interpolation
var blended = color.blend(c_rgba, k);
var interpolated = color.lerp(r, b, 0.5);

// 5. Perceptual Transforms
print("Yellow Luminance: " + color.luminance(y));
var inverted_blue = color.invert(b);
var gray_yellow = color.grayscale(y);

// 6. Tonal and Saturation Adjustments
var lighter = color.lighten(c_hex, 0.15);
var darker = color.darken(c_hex, 0.15);
var saturated = color.saturate(c_hex, 0.2);
var desaturated = color.desaturate(c_hex, 0.2);

// 7. Distance
var dist = color.distance(w, k);
print("Distance White to Black: " + dist);
```

# Coroutine #
A coroutine wraps a function so it can pause mid execution with ```yield``` and pick back up later exactly where it left off. The yield documentation is in [Syntax.md](syntax.md) in the [Coroutines](syntax.md#coroutines) section
 
**Added in v0.2.0**
- ```coroutine.create(fn)``` // Wraps a lambda or zero-arg-function in a coroutine and returns a handle to it. The coroutine doesn't run until the first ```coroutine.resume```
- ```coroutine.resume(handle)``` // Runs the coroutine until it either hits a ```yield``` or finishes. Returns the yielded value or the function's return value once it's done while it's still running, ```coroutine.status``` has this information. Throws a runtime error if called on a coroutine that's already ***dead***.
- ```coroutine.status(handle)``` // Returns **```"suspended"```** (paused at a yield), **```"running"```**, or **```"dead"```** (finished, cannot be resumed again)
- ```coroutine.is_done(handle)``` // Returns true if the coroutine has finished (same as ```coroutine.status(handle) == "dead"```), otherwise false
- ```coroutine.free(handle)``` // Frees the memory of a coroutine, **```Returns true if successful and throws a runtime error if else```**
- ```coroutine.kill(handle)``` // **```Added in v0.3.0:```** Frees the memory of a coroutine running all destructors and destroying all state, **```returns true if successful and throws a runtime error if else```**
- Example, a coroutine that yields three times, plus a basic **```sleep```** function:
```slate
fn counter() {
    var i = 0;
    while (i < 3) {
        yield i;
        i = i + 1;
    }
}
 
var co = coroutine.create(counter);
while (coroutine.status(co) != "dead") /*can be written as "while(!(coroutine.is_done(co))) { code }"*/ {
    print(coroutine.resume(co));
}
coroutine.free(co);
 
fn sleep(seconds) {
    var wake_at = os.time() + seconds;
    while (os.time() < wake_at) {
        yield 0;
    }
}
```

# Class #

**Added in v0.3.0**
- ```class.has(class_instance, field)``` // Returns true if `class_instance` has a field named `field` (public or private), otherwise false
- ```class.has_method(class_instance, method_name)``` // Returns true if `class_instance`'s class defines a method named `method_name`, otherwise false
- ```class.is_private(class_instance, field)``` // Returns true if `field` is a private field of `class_instance`'s class, otherwise false
- ```class.is(class_instance, type_name)``` // Returns true if `class_instance` is an instance of the class named `type_name`, otherwise false
- ```class.name(class_instance)``` // Returns the class name of `class_instance` as a string, or `""` if it isn't a class instance
- ```class.fields(class_instance)``` // Returns an **array of field name strings** for `class_instance` **(order not guaranteed)**
- ```class.methods(class_instance)``` // Returns an **array of method name strings** defined on `class_instance`'s class **(order not guaranteed)**

# Struct #

**Added in v0.4.0**
- ```struct.has(struct_instance, field)``` // Returns true if `struct_instance` has a field named `field`, otherwise false
- ```struct.name(struct_instance)``` // Returns the struct name of `struct_instance` as a string, or `""` if it isn't a struct instance
- ```struct.is(struct_instance, type_name)``` // Returns true if `struct_instance` is an instance of the struct named `type_name`, otherwise false
- ```struct.fields(struct_instance)``` // Returns an **array of field name strings** for `struct_instance`, returns a empty array if `struct_instance` is not a struct or was null **(order not guaranteed)**
- ```struct.create(name)``` // Returns a new bare struct instance with the specified `name` and no fields
- ```struct.set(struct_instance, field, value)``` // Sets `field` to `value` on `struct_instance` in-place, creating it if it doesn't exist, and returns the struct with the set field
- ```struct.remove(struct_instance, field)``` // Removes `field` from `struct_instance`, returns true if the field was successfully removed, otherwise false
- ```struct.get(struct_instance, field)``` // Returns the value of `field` on `struct_instance`, or null if `struct_instance` is invalid or the field does not exist

# Compression #

**Added in v0.4.0**
- ```compression.deflate_compress(value, level)``` // Compresses a value using DEFLATE with an optional compression level (0–9). Unsupported types: (classes, closures, functions, pointers, struct types **(not a struct value)**, and class types) return null
- ```compression.deflate_decompress(data)``` // Decompresses a DEFLATE-compressed binary string back into a value
- ```compression.lz4_compress(value, level)``` // Compresses a value using LZ4 with an optional level (1–12 for High Compression, or <= 0 for default fast speed). Unsupported types **(the above ones)** return null
- ```compression.lz4_decompress(data)``` // Decompresses an LZ4-compressed binary string back into a value
- ```compression.zstd_compress(value, level)``` // Compresses a value using Zstandard with an level (1–22). Unsupported types **(the above ones)** return null. Is multithreaded.
- ```compression.zstd_decompress(data)``` // Decompresses a Zstandard-compressed binary string back into a value
- ```compression.lzma_compress(value, level)``` // Compresses a value using LZMA (XZ) with an level (0–9). Unsupported types **(the above ones)** return null. Is multithreaded.
- ```compression.lzma_decompress(data)``` // Decompresses an LZMA-compressed binary string back into a value

# Bitwise #

**Added in v0.4.0**
- ```bitwise.and(a, b)``` // Performs a bitwise **AND** operation on two 64-bit integers (`a & b`)
- ```bitwise.or(a, b)``` // Performs a bitwise **OR** operation on two 64-bit integers (`a | b`)
- ```bitwise.xor(a, b)``` // Performs a bitwise **XOR** operation on two 64-bit integers (`a ^ b`)
- ```bitwise.not(a)``` // Performs a bitwise **NOT** (one's complement) operation on a 64-bit integer (`~a`)
- ```bitwise.shl(a, b)``` // Performs a bitwise **left shift** on integer `a` by `b` bits (`a << b`)
- ```bitwise.shr(a, b)``` // Performs a bitwise **right shift** on integer `a` by `b` bits (`a >> b`)

# Type #
- ```type.is_int(val)``` // Returns true if the value is an integer, otherwise false
- ```type.is_double(val)``` // Returns true if the value is a double, otherwise false
- ```type.is_number(val)``` // Returns true if the value is either an integer or a double, otherwise false
- ```type.is_string(val)``` // Returns true if the value is a string, otherwise false
- ```type.is_bool(val)``` // Returns true if the value is a boolean, otherwise false
- ```type.is_array(val)``` // Returns true if the value is an array, otherwise false
- ```type.is_struct(val)``` // Returns true if the value is a struct, otherwise false
- ```type.is_class(val)``` // Returns true if the value is a class, otherwise false
- ```type.is_function(val)``` // Returns true if the value is a function **(any type of function)**, otherwise false
- ```type.is_pointer(val)``` // Returns true if the value is a pointer, otherwise false
- ```type.is_null(val)``` // Returns true if the value is null, otherwise false
- ```type.name(val)``` // Returns the type name of the value as a string **```("bool", "int", "double", "string", "pointer", "null", "struct_type", "class_type", "function", "class", "struct", "array", and if none it returns "unknown")```**
- ```type.double_to_int(num)``` // Converts a double to a 64-bit integer
- ```type.int_to_double(num)``` // Converts a 64-bit integer to a double
- ```type.to_string(val)``` // Converts a value (int, double, string, bool) to their string representation
- ```type.string_to_number(str)``` // Returns a number coming from a string, returning null if it fails

**Added in v0.3.0**
- ```type.to_display_string(val)``` // Returns a formatted string of any type of value

# Slate #
- ```slate.version()``` // Returns the slate version

**Added in v0.3.0**
- ```slate.evaluate(code)``` // Executes and returns the return value from code (or 0 if no return value)
