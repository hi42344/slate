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

// there is also the Ternary operator like C/C++
```
- There is continue and break keywords, continue skips the rest of the loop and break stops it.
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

# Comments #
- single line ```// ```
- multiline ```/* */```

# Basic Structures #
**Structs**
```slate
struct vector2 {
    var a = 5; // Default values
    var b = 5; // Default values, if no values are set in either the struct or initialization then the value will be 0
    b; // Starts at 0

    // Functions/other things are not supported in structs, you must use a class for those
} 

var struct_a = vector2(100, 1); // Overwritting defaults, goes in order
print(struct_a.a); // prints 100
print(struct_a.b); // prints 1
```
**Enums**
```slate
enum name {
    something_1;
    something_2 = 100;
    something_3;
    something_4 = 3;
    something_5;
}

var a = name.something_1;
var b = name.something_2;
var c = name.something_3;
var d = name.something_4;
var e = name.something_5;
print(a); // 0 since it has no value set and is at the first index
print(b); // 100
print(c); // 101 since it's 1 more than the last value unless set
print(d); // 3 since it's set
print(e); // 4 since it's 1 more than the last
// Rule is that a enum is always 1 more than the last value
```
**Namespaces**
```slate
//Note that if there is random code inside a namespace like "print("hello world")" then it will execute
namespace math {
    fn factorial(n) {
        var result = 1;
        for (var i = 2; i <= n; i += 1) {
            result *= i;
        }
        return result;
    }
}
// You use the "." scope resolution operator for all scopes
print(math.factorial(5));
```

# Pointers and References #
- Deletion ```var b = &a; delete b; /*deletes a*/, var a = make(5); delete a; var b = 5; delete b; (deletion can be done on anything, even normal variables that get auto deleted after scope)```
- Assigment ```var ptr = make(5); // this will make a new pointer with the value of 5```
- dereferencing ```*ptr``` Note that if you are getting a field you must wrap this in (*ptr) or you will get errors
- referencing ```var a = 10; var b = &a; // b is now a, you dont need to use "make(&a)" as that also doesnt work```
*functions*
- Passing in a refrence of a variable lets the function have/modify the actual value, you do not need to use the * dereference operator unless it's a pointer you pass in. ex:
```slate
fn set(a, new_value) {
    a = new_value;
}

var test = 100;
set(test, 0);
print(test); // prints 100 since the function made a copy
set(&test, 0);
print(test); // prints 0
// pointer example
fn set_ptr(ptr_a, new_value) {
    *ptr_a = new_value; // if no * dereference operator printing "ptr" will print 0
}
var ptr = make(100);
set_ptr(&ptr, 5); // must still pass in the refrence 
print(*ptr); // prints 5
// Like other languages I dont recommend using pointers a lot of the time, a refrence does most of what you need anyway
```

# Strings #
- Reading ```string[index] // Runtime error if out of range```

*Properties/methods*
- .length ```// Returns the size/length of the string```
- .append(content) ```// Returns a new string with the contents appended```
- .insert(content, index) ```// Returns a new string with the inserted content```
- .at(index) ```// Returns null if out of range```

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

# Classes #
- Makes deep copies by default
- Note that you should always use ```this.something``` instead of ```something``` inside a class
- Note that there is no Polymorphism or Inheritance
- There is only public and private access modifiers

*Example code*
```slate
class person {
    private:
        var a = 5;
        b;
    public:
        person(value) {
            this.a = value;
            print("constructed");
        }
        !person() {
            print("deconstructed");
        }

        copy() {
            print("copied");
        }
        assignment(new_value) {
            print("assigned");
        }
        referenced() {
            print("referenced");
        }
        dereferenced() {
            print("dereferenced");
        }
        // methods
        fn set(new_value) {
            this.a = new_value;
        }

        fn get() {
            return this.a;
        }
}
if(true) {
    var a = person(10); // prints constructed
    var b = make(person(10.100)); // prints constructed     
    print((*b).get()); // prints derferenced and 10.1
    print(a.get()); // prints 10;
    a.set(100);
    print(a.get()); // prints 100;
    var b = a; // prints copied
    var c = &a; // prints referenced
    a = null; // prints assigned
} // prints deconstructed 2x // Note that even if a class gets reassigned it's deconstructer will activate
```
