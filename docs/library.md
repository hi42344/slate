# The built in c++ library's #

- ```print(contents)``` // prints whatever is in it, eg: ```print("hello world" + 5);``` this prints "hello world5" and a new line.

# Math #
- ```math.abs(number);``` // Returns the absolute value of a number
- ```math.acos(number);``` // Returns the arc cosine of a number in radians
- ```math.asin(number);``` // Returns the arc sine of a number in radians
- ```math.atan(number);``` // Returns the arc tangent of a number in radians
- ```math.atan2(y, x);``` // Returns the arc tangent of y/x in radians using signs to determine the quadrant
- ```math.ceil(number);``` // Rounds a number upward to the nearest integer
- ```math.cos(number);``` // Returns the cosine of an angle in radians
- ```math.cosh(number);``` // Returns the hyperbolic cosine of a number
- ```math.deg(radians);``` // Converts an angle from radians to degrees
- ```math.exp(number);``` // Returns e raised to the power of a number
- ```math.floor(number);``` // Rounds a number downward to the nearest integer
- ```math.fmod(x, y);``` // Returns the floating-point remainder of x/y
- ```math.huge();``` // Returns positive infinity
- ```math.log(number);``` // Returns the natural logarithm (base e) of a number
- ```math.log10(number);``` // Returns the common logarithm (base 10) of a number
- ```math.max(x, y);``` // Returns the larger of two values
- ```math.min(x, y);``` // Returns the smaller of two values
- ```math.pi();``` // Returns the mathematical constant pi (3.14159265358979323846)
- ```math.pow(base, exp);``` // Returns the base raised to the power of the exponent
- ```math.rad(degrees);``` // Converts an angle from degrees to radians
- ```math.sin(number);``` // Returns the sine of an angle in radians
- ```math.sinh(number);``` // Returns the hyperbolic sine of a number
- ```math.sqrt(number);``` // Returns the square root of a number
- ```math.tan(number);``` // Returns the tangent of an angle in radians
- ```math.tanh(number);``` // Returns the hyperbolic tangent of a number
- ```math.random(min, max);``` // Generates a pseudo-random double between min and max
- ```math.random_seeded(min, max, seed);``` // Generates a pseudo-random double between min and max using a seed
- ```math.sign(number);``` // Returns 1 for positive, -1 for negative, or 0 for zero
- ```math.clamp(value, min, max);``` // Restricts a value to be between a minimum and maximum range
- ```math.round(number);``` // Rounds a number to the nearest integer
- ```math.lerp(a, b, t);``` // Linearly interpolates between a and b by t
- ```math.map(value, in_min, in_max, out_min, out_max);``` // Linearly maps a value from an input range to an output range
- ```math.noise(x, y, z);``` // Generates 3D Perlin noise based on the input coordinates x, y, and z

# os #
- ```os.sleep(time)``` // sleeps the program for the time in seconds
- ```os.throw(message)``` // throws/crashes the program and prints the message
- ```os.platform()``` // Returns the current platform, eg: ```"windows", "linux", "macos", "ios", "android"``` else ```"unknown"```
- ```os.time()``` // Returns the time **(in seconds)** since the **computer has turned on** or **epoch time**
- ```os.clock()``` // Returns the CPU time (in seconds) since the program has started
- ```os.date()``` // Returns a locally formatted string of the current date and time
- ```os.date_time_year()``` // Returns the current time and year formatted as "Hours:Minutes:Seconds Year"
- ```os.date_time()``` // Returns the current time formatted as "Hours:Minutes:Seconds"
- ```os.getenv(var)``` // Returns the value of an environment variable, or an empty string if not found
- ```os.file_save(path, content)``` // Saves content to a file (overwriting if it exists), returns true if successful
- ```os.file_load(path)``` // Returns the entire contents of a file as a string
- ```os.file_exists(path)``` // Returns true if a file or directory exists at the path, otherwise false
- ```os.file_delete(path)``` // Deletes a file or empty directory, returns true if successful
- ```os.file_size(path)``` // Returns the size of a file in bytes, or -1 if the file is not found
- ```os.file_append(path, content)``` // Appends content to the end of a file, returns true if successful
