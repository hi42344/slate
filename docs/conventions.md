# Language Conventions #
**These are just guidelines, so while i recommend you follow them, you dont have to follow them exactly.**

## General code
- Code should have fallbacks by default unless you know something can't be **null**, eg: ```if(something) { print(something); }```.

## Functions/methods
- Functions should throw a error by default if not possible.
- Functions should have a **safe** way to do something if necessary, eg: ```array[index]``` *unsafe* **vs** *safe* ```array.at(index)```.
- Functions with a safe varient should always **return **null** as a fallback** and should always be **understandable** that they're safe with a clear suffix

## Naming conventions
- Use snake_case.
- Use upper snake_case for constants, eg: ```var PI = 3.1415926535897932;```.
