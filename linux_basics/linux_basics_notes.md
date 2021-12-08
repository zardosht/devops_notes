# The Linux Basics Course

* Working with Shell
* Linux core concepts
* Package Management
* Shell & Bash
* Security and file permissions
* Linux Networking
* Storage in Linux
* SystemD and Services

# Working with Shell 

* REPL: Read-Eval-Print Loop
* Command, Argument, Options (aka. switches, flags)
* `echo Hello`, `echo -n Hello` omits the new line
* `uptime`
* Man pages: command help (manual)
* Command types: 
  * Internal: Are part of the shell itself and come bundled with it
    * There are around 30 internal commands
    * `echo`, `cd`, `pwd`, `mkdir`, `set`, ...
  * External: Are binary programs or scripts that are installed in different locations on the systems
    * They usually are installed using the Linux Distribution's package manager or can be created or installed by user
  * `type <command>` tells if a command is internal or external

## Basic Linux Commands

* `pwd`: present working directory, shows the current directory where you are
* `ls`
* `mkdir`: can create multiple directories in one command
  * `mkdir <dir1> <dir2> <dir3>`
  * `mkdir -p <dir1>/<dir1>/<dir3>`: creates the dir structure including parents
* `cd`, `cd ..`
* Absolute path vs relative path
* Root directory `\`
* `pushd <dir1>`: push current directory onto the `DIRSTACK` bash variable (the directory stack of remembered directories) and then changes to `dir1`
* `dirs`: shows the contents of `DIRSTACK`, the remembered directories
* `popd`: With  no  arguments,  removes  the  top directory  from  the stack, and performs a `cd` to the new top directory.
  
* `mv`: move or rename
* `cp`: copy
* `rm`: remove
* to copy or remove a dir use `-r` (for recursive) switch

* `cat <file>`: print content of the file
* `cat > <file>`: shows the prompt and you can type and the press `Ctrl-D` to write the content into the file
* `touch`: create a file
* Pagers: `more`, `less`:
  * space: scroll one page
  * enter: scroll one line
  * b: to go to previous pages
  * /: to search fo a pattern
  * q: to exit
  * `more` loads entire file at once, which might not be a good option
  * `less` also allows scrolling using arrow keys

* `ls -al`: long list, and show hidden files
* `ls -lt`: list all files sorted on last modified date, use `ls -ltr` for reverse order

## Getting Help

* `whatis`: displays a one line help of what a command does
* `man`: shows man pages of a command
* `--help`, `-h`: most commands have this option to show help
* `apropos`: searches through man page names and descriptions for a given keyword, useful when you want to look up all commands that contain a specific keyword

