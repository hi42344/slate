# Variable Creation #
>Dynamically typed
- Keyword ```var```
- Declaration ```var name = value;```
- Usage ```name = value;```, ```print(name);```
- **Five basic types**
- *long long* ```var name = 10;```
- *double* ```var name = 10.5;```
- *string* ```var name = "hello world";```
- *boolean* ```var name = true;```
- *null* ```var name = null;```

# Control flow #

- **if statements**
```slate
if(condition/conditions) {
    code
}

elif(condition/conditions) {
    code
}

else {
    code
}
```
- **For loops (C/C++ style)**
```slate
for(initialization; condition; update) {
    code
}
```
- **While loops (C/C++ style)**
```slate
while(condition/conditions) {
    code
}
```
# Functions #
```slate
fn function_name(params) {
    [code]
}
```
- **Example**
```slate
fn add(a, b) {
    return a + b;
}
```
- **Calling**
```slate
function_name(params)
```
# Operators #
- +, -, *, /, %
- +=, -=, /=, *=

  *Logical*
- &&, ||, !

  *Comparison*
- '>, <, ==, !=, <=, >=

# Arrays #
- Assignment: ```var array = [1, 2, 3, 4, 5];```
- Reading ```array[index] // Runtime error if out of range```
- Writing ```array[index] = value; // Runtime error if out of range```

  *Properties/methods*
- .length ```// Returns the size/length of the array```
- .at(index) ```// Returns null if out of range```
- .push(value); ```// like c++ vector.push_back, grows array```
- .pop(); ```// like c++ vector.pop_back, array will stay the same capacity, size will shrink, Runtime error if array is empty```
- .resize(new_size); ```// like c++ vector.resize(), Deletes anything at a bigger index than the new size```
- .insert(index, value) ```// like c++ vector.insert()```
- .remove(index) ```// like c++ vector.erase(), returns the deleted value at the index```

  *Behavior*
- Makes a copy by default for variables
```slate
var a = [1, 2, 3, 4];
var b = 5;
a[0] = b;
a[0] = 100;
print(b); // prints 5 since b in the array is a copy
```
- You can pass a variables reference to not make a copy
```slate
var a = [1, 2, 3, 4];
var b = 5;
a[0] = &b;
a[0] = 100;
print(b); // prints 100 since b is actually in the array
```
