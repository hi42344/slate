# Core libraries #
 
### Table of Contents
 
| Library | Description | Quick Link |
| :--- | :--- | :--- |
| **Print** | Console output | [Print](#core-libraries) |
| **Math** | Math | [Math](#math) |
| **OS** | File, clock, times | [OS](#os) |
| **Input** | Keyboard and Mouse utilities | [Input](#input) |
| **Data** | Easy data saving | [Data](#data) |
| **Coroutine** | Concurrency | [Coroutine](#coroutine) |
| **String** | String and hashing utilities | [String](#string) |
| **Array** | Array utilities | [Array](#array) |
| **Type** | Type checking and casting | [Type](#type) |
| **Slate** | Language data | [Slate](#slate) |

- ```print(contents)``` // prints whatever is in it, eg: ```print("hello world" + 5);``` this prints "hello world5" and a new line.

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

# Os #
- ```os.sleep(time)``` // sleeps the program for the time in seconds
- ```os.throw(message)``` // throws/crashes the program and prints the message
- ```os.platform()``` // Returns the current platform, eg: **```"windows", "linux", "macos", "ios", "android"```** else **```"unknown"```**
- ```os.time()``` // Returns the time **(in seconds)** since the **computer has turned on** or **epoch time**
- ```os.clock()``` // Returns the CPU time **(in seconds)** since the program has started
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

# Input #

**Added in v0.2.0**

**The string keys**
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
- The three mouse buttons are: "left", "right", "middle"
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
- ```input.mouse_toggle_pressed(handle)``` // Returns true only on the frame ```button``` goes from up to down, otherwise false — call once per loop/coroutine resume
- ```input.free_mouse_toggle(handle)``` // Frees the memory of a mouse toggle, **```Returns true if successful and false if else```**

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
var random_save_num = type.double_to_int(math.round(math.random(1, 3)));
data.save(map, SaveManager, random_save_num);

var map2 = data.load(SaveManager, 1);
print(data.read(map2, "hp", random_save_num));
```

# String #
- ```string.charCode(string, index)``` // Returns the ASCII value of the character at the index, Runtime error if out of bounds
- ```string.sub(string, start, end)``` // Returns a substring from the start index to the end index, auto clamps index and **supports negative indexing**, ```-1 is the last character, -2 is the second to last, etc```
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

# Array #
 
**Added in v0.2.0**
- ```array.contains(array, value)``` // Returns true if ```value``` is found anywhere in ```array```, otherwise false
- ```array.index_of(array, value)``` // Returns the **index of the first occurrence** of ```value``` in ```array```, or -1 if not found
- ```array.sort(array)``` // Sorts ```array``` **in place** in ascending order **(numbers and strings only)**, **```Returns true if successful and false if else```**
- ```array.sort_by(array, comparator)``` // Sorts ```array``` **in place** using ```comparator(a, b)```, a function returning true if ```a``` should come before ```b```, **```Returns true if successful and false if else```**
- ```array.reverse(array)``` // Reverses ```array``` **in place**, **```Returns true if successful and false if else```**
- ```array.slice(array, start, end)``` // Returns a **new array** containing the elements from the start index to the end index, auto clamps index and **supports negative indexing**, ```-1 is the last element, -2 is the second to last, etc```
- ```array.concat(array1, array2)``` // Returns a **new array** containing every element of ```array1``` followed by every element of ```array2```

# Coroutine #
A coroutine wraps a function so it can pause mid execution with ```yield``` and pick back up later exactly where it left off. The yield documentation is in [Syntax.md](syntax.md) in the [Coroutines](syntax.md#coroutines) section
 
**Added in v0.2.0**
- ```coroutine.create(fn)``` // Wraps a lambda or zero-arg-function in a coroutine and returns a handle to it. The coroutine doesn't run until the first ```coroutine.resume```
- ```coroutine.resume(handle)``` // Runs the coroutine until it either hits a ```yield``` or finishes. Returns the yielded value or the function's return value once it's done while it's still running, ```coroutine.status``` has this information. Throws a runtime error if called on a coroutine that's already ***dead***.
- ```coroutine.status(handle)``` // Returns **```"suspended"```** (paused at a yield), **```"running"```**, or **```"dead"```** (finished, cannot be resumed again)
- ```coroutine.is_done(handle)``` // Returns true if the coroutine has finished (same as ```coroutine.status(handle) == "dead"```), otherwise false
- ```coroutine.free(handle)``` // Frees the memory of a coroutine, **```Returns true if successful and false if else```**
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
- ```type.name(val)``` // Returns the type name of the value as a string **```("int", "double", "string", "pointer", "null", "struct_type", "class_type", "function", "class", "struct", "array", and if none it returns "unknown")```**
- ```type.double_to_int(num)``` // Converts a double to a 64-bit integer
- ```type.int_to_double(num)``` // Converts a 64-bit integer to a double
- ```type.to_string(val)``` // Converts a value (int, double, string, bool) to their string representation
- ```type.string_to_number(str)``` // Returns a number coming from a string, returning null if it fails

# Slate #
- ```slate.version()``` // Returns the slate version
