# Keywords #
| Keyword | Section |
|---|---|
| `//` / `/**/` | [Comments](#comments) |
| `[]` | [Arrays](#arrays) |
| `"string"` | [Strings](#strings) |
| `var` | [Variable Creation](#variable-creation) |
| `fn` | [Functions](#functions) |
| `if` / `elif` / `else` | [Control flow](#control-flow) |
| `while` | [Control flow](#control-flow) |
| `for` | [Control flow](#control-flow) |
| `break` / `continue` | [Control flow](#control-flow) |
| `struct` | [Basic Structures](#basic-structures) |
| `enum` | [Basic Structures](#basic-structures) |
| `namespace` | [Basic Structures](#basic-structures) |
| `class` | [Classes](#classes) |
| `make` / `delete` / `&` / `*` | [Pointers and References](#pointers-and-references) |
| `import` | [Imports](#imports) |

# imports #
- import "path.slate" // Goes to the librarys folder first (my_library) or (folder(or folders)/my_library) otherwise just uses the path
- import "path.slate" as namespace_name // imports and wraps everything in a namespace
- Auto manages infinite imports like ex: ```import "otherlibrary.slate"``` and inside ```otherlibrary.slate``` it imports ```librarythatimported.slate```
- **No linking or any other library annoyances required**

# Variable Creation #
- Keyword ```var```
- Declaration ```var name = value;```
- Usage:
```slate
name = value;
print(name);
```

**Five basic types**
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
**Lambdas**
- Not named functions, use the `fn` keyword directly
```slate
var add = fn(a, b) {
    return a + b;
};
print(add(2, 3)); // prints 5
```
- Commonly passed directly as an argument:
```slate
fn apply(value, transform) {
    return transform(value);
}
print(apply(10, fn(x) {
    return x * 2; // prints 20
}));
```
- **Closures**: a lambda captures the enclosing function's variables by reference at the moment it's created. Later changes to the captured variable are visible through the closure, and each call gets its own independent capture
```slate
fn make_adder(offset) {
    return fn(base) {
        return base + offset;
    };
}
var add5 = make_adder(5);
var add100 = make_adder(100);
print(add5(10));   // 15
print(add100(10)); // 110
```
# Operators #
- +, -, *, /, %
- +=, -=, /=, *=

**Logical**
- &&, ||, !

**Comparison**
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
**Deletion**
```slate
var b = &a; delete b; /*deletes a*/
var a = make(5); delete a;
var b = 5; delete b; // deletion can be done on anything, even normal variables that get auto deleted after scope
```
Usage after deletion will give a error ["Runtime Error: Undefined variable 'variable name'"]

**Example**
```slate
var a = 5;
delete a;
print(a); // "Runtime Error: Undefined variable 'a'" error
```

- Assigment ```var ptr = make(5); // this will make a new pointer with the value of 5```
- dereferencing ```*ptr``` Note that if you are using a field you must wrap (*ptr) or you will get errors
- referencing ```var a = 10; var b = &a; // b is now a, you dont need to use "make(&a)" as that also doesnt work```

**functions**
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
set_ptr(&ptr, 5); // must still pass in the refrence, everything makes a reference
print(*ptr); // prints 5

// Note that passing a reference (&x) of a regular variable and then dereferencing it (*param) does
// not write through to the original variable, only a pointer supports
// this. If you passed a reference, just assign directly (param = new_value;)
```

# Strings #
- Reading ```string[index] // Runtime error if out of range```

**Properties/methods**
- .length ```// Returns the size/length of the string```
- .append(content) ```// Returns a new string with the contents appended```
- .insert(content, index) ```// Returns a new string with the inserted content```
- .at(index) ```// Returns null if out of range```

# Arrays #
- Assignment: ```var array = [1, 2, 3, 4, 5];```
- Reading ```array[index] // Runtime error if out of range```
- Writing ```array[index] = value; // Runtime error if out of range```

**Properties/methods**
- .length ```// Returns the size/length of the array```
- .at(index) ```// Returns null if out of range```
- .push(value); ```// like c++ vector.push_back, grows array```
- .pop(); ```// like c++ vector.pop_back, array will stay the same capacity, size will shrink, Runtime error if array is empty```
- .resize(new_size); ```// like c++ vector.resize(), Deletes anything at a bigger index than the new size```
- .insert(index, value) ```// like c++ vector.insert()```
- .remove(index) ```// like c++ vector.erase(), returns the deleted value at the index```

**Behavior**
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

**Classes have 6 default methods**
- Constructer // class name
- Deconstructor // class name with a ! before it, eg: "!person()"
- Copied // in code it's the "copy()" method
- Assigned // in code it's the "assignment(new_value)" method // note that you cant use "new_value" thats just one of the language's quirks
- Referenced (lowercase in code)
- Dereferenced (lowercase in code)

**Example code**
```slate
class person {
    private:
        var a = 5;
        b;
    public:
        // Native methods
        person(value /*A class constructer can have as many params as wanted*/) {
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
        /*Added in version 0.2.0 you can use the new value and return inside the assignment function to change what gets assigned
        eg: "return new_value * 2;" or "print(new_value);" */
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
