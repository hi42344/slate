## Slate ##
A dynamically typed interpreted language with lua/rust/cpp syntax

>**Note:** Slate is currently in development. All features are subject to change

# HOW TO USE #
- [Download the binary](https://github.com/hi42344/slate/releases/latest) and open it
- Make a script inside the scripts folder with the ```.slate``` file extension (or anywhere but you'd have to use the file path)
```lua
print("hello world");
```
- Open a terminal and type ```"slate script_name"```, this will run it immediately

**Additional features**
- You can compile something by doing ```"slate script_name --compile"``` or ```"--c"```
- Compiled files don't depend on any libraries they used to need, a compiled file will always run as long as it's valid Slate
- Running a compiled file is the same ```"slate script_name"``` (if you don't put a file extension, Slate always looks for a compiled file with the same name first, e.g. ```"script.slatebin"``` before ```"script.slate"```)

**Flags**
```bash
- "--compile" / "--c" to compile a .slate file
- "--bytecode" / "--b" to see the compiled bytecode
- "slate --version" / "--v" to see what version you are on
- "slate --license" / "--l" added in v0.2, gives the link to the "license's" folder
```

**Notes**
- The only ```falsely``` things are null and false
- Classes must always use this.field for anything inside a class

# WHERE IT IS #

**WINDOWS**
```ini
Executable Location:       C:\Developer\slate\bin\slate.exe
Default Scripts:           C:\Developer\slate\Scripts\
Default Libraries:         C:\Developer\slate\Libraries\
Path Added To:             HKEY_CURRENT_USER\Environment\Path
```

**LINUX**
```ini
Executable Location:       ~/.local/bin/slate
Default Scripts:           ~/.local/share/slate/scripts/
Default Libraries:         ~/.local/share/slate/libraries/
Path Added To:             ~/.bashrc
```

**MACOS**
```ini
Executable Location:       ~/.local/bin/slate
Default Scripts:           ~/.local/share/slate/scripts/
Default Libraries:         ~/.local/share/slate/libraries/
Path Added To:             ~/.zshrc
```
# Documentation
- [Syntax](./docs/syntax.md)
- [Native libraries](./docs/library.md)
- [Conventions](./docs/conventions.md)
