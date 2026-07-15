# slate
Interpreted language with lua/python/cpp syntax

HOW TO USE:
- Download the binary and open/start it
- Make a script inside the scripts folder (or anywhere but you'd have to manually use the file path)
- print("hello world");
- Open a terminal and type "slate script_name", this will compile it and run it immediately
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
# Additional features #
- You can only compile something by doing "slate script_name --compile" or "--c"
# Note that if you dont add a file extension it will always run the compiled files if they exist # 
- You can run that compiled file by doing "slate script_name"
# Flags #
- "--compile" to compile
- "--bytecode" to see the compiled bytecode
- "slate --version" to check your version
# Short flags #
- "--c" to compile
- "--b" to see the compiled bytecode
- "slate --v" to check your version

WHERE IT IS:
WINDOWS:
- Executable Location:       C:\Developer\slate\bin\slate.exe
- Default Scripts:           C:\Developer\slate\Scripts\
- Default Libraries:         C:\Developer\slate\Libraries\
- Path Added To:             HKEY_CURRENT_USER\Environment\Path
# Not Cross platform yet, only windows since i don't know how to cross compile
LINUX:
- Executable Location:       ~/.local/bin/slate
- Default Scripts:           ~/.local/share/slate/scripts/
- Default Libraries:         ~/.local/share/slate/libraries/
- Path Added To:             ~/.bashrc
# Not Cross platform yet, only windows since i don't know how to cross compile
MACOS:
- Executable Location:       ~/.local/bin/slate
- Default Scripts:           ~/.local/share/slate/scripts/
- Default Libraries:         ~/.local/share/slate/libraries/
- Path Added To:             ~/.zshrc







