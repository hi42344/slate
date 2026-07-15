# Syntax # 
**Variable Creation**
>Dynamically typed
- Keyword ```var```
- Declaration ```var name = value;```
- Usage ```name = value;```, ```print(name);```
- **Four basic types**
- *long long* ```var name = 10;```
- *double* ```var name = 10.5;```
- *string* ```var name = "hello world";```
- *boolean* ```var name = true;```

**Functions**
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
**Operators**
- +, -, *, /, %
- +=, -=, /=, *=

  *Logical*
- &&, ||, !

  *Comparison*
- '>, <, ==, !=, <=, >=

**Arrays**
- Makes a copy by default for variables, eg: 
```slate
var a = [1, 2, 3, 4];
var b = 5;
a[0] = b;
a[0] = 100;
print(b); // prints 5 since b in the array is a copy
```
You can pass a variables reference to not make a copy, eg:
```slate
var a = [1, 2, 3, 4];
var b = 5;
a[0] = &b;
a[0] = 100;
print(b); // prints 100 since b is actually in the array
```
