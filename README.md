## Slate ##
A dynamically typed interpreted language with lua/rust/cpp syntax

>**Note:** Slate is currently in development. All features are subject to change

# HOW TO USE #
- Download the binary and open it
- Make a script inside the scripts folder with the ```.slate``` file extension (or anywhere but you'd have to use the file path)
```lua
print("hello world");
```
- Open a terminal and type ```"slate script_name"```, this will compile it and run it immediately

**Additional features**
- You can compile something by doing ```"slate script_name --compile"``` or ```"--c"```
- Compiled files dont need any librarys they used to exist, a compiled file will always run as long as it's valid slate
- You can run that compiled file by doing ```"slate script_name"``` (if you dont add a file extension it will always run compiled files that have the same name first like ```"script.slatebin"``` instead of ```"script.slate"```)

**Flags**
```bash
- "--compile" / "--c" to compile a .slate file
- "--bytecode" / "--b" to see the compiled bytecode
- "slate --version" / "--v" to see what version you are on
```

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
