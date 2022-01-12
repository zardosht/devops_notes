# The Linux Basics Course

* https://github.com/kodekloudhub/linux-basics-course

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

* https://github.com/kodekloudhub/linux-basics-course


## Bash Shell

* Bourne Shell (`sh`) developed in 1970s for Unix and still in use today, C Shell (`csh` or `tcsh`), Korn Shell (`ksh`), Z Shell (`zsh`), Bourne Again Shell (`bash`)
* Different shells may have different features and facilities, but they all serve the same goal: to facilitate communication between user and the operating system
* `echo $SHELL` shows the current (default) shell being used
* Bash is one of the most popular shells, because of the features like auto-completion and brace expansion which is not available in shells like Bourne Shell
* `chsh` to change the default shell; it takes effect when you open a new terminal

### Bash shell features:
* Auto-completion
* Aliases: `alias dt=date`
* History: `history`
* Environment variables: store information about user's login session that are used by the Shell when executing commands
  * e.g. `$SHELL` or `$HOME`
  * `env` to list all the environment variables
  * `export` to set a new environment variables, e.g. `export OFFICE=munich`; This will set the variable for the current shell or any other process started by the shell
  * You can also assign a variable with `export`, like simple `OFFICE=munich`. However this will only assign the variable within the shell and the value is not carried forward to any other process
  * to make the environment variables persistent over subsequent logins or reboots add them to `~/.profile` or `~/.pam_environment` file
  * `echo $LOGNAME`
  * `echo $TERM`


* `$PATH`: paths to search for the external commands
* `which` command to check if the location of a command can be identified
* `export PATH=$PATH:/opt/obj/bin` to extend the PATH

### Customizing the Bash Prompt
* `[~]$` bash prompt can be customized to show different information, for example the logged-in user and the host name
* The bash prompt is set and controlled by a set of specific environment variables, the most common of them is `$PS1` for primary prompt
* `echo $PS1`, prints for example `[\W]$` prints `[current working directory]$`
* check the documentation for different directives you can use in `$PS1` to change the prompt: 
  * `\d`: the date in Weekday Month Date format
  * `\e`: an ASCII escape character (033)
  * `\h`: the hostname HDQN
  * `\n`: new line
  * `\r`: carriage return
  * `\s`: the name of the shell
  * `\u`: username of the current user
  * `\w`: current working directory
  * `\$`: if effective UID is 0 prints a `#` otherwise a `$`


# Linux Core Concepts

## The Linux Kernel





## Working with Hardware



## Linux Boot Sequence




## Runlevels





## File Types



## File System Hierarchy


