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

* https://www.cs.ait.ac.th/~on/O/oreilly/unix/upt/ch08_19.htm

# Working with Shell 

* https://www.vanimpe.eu/2014/01/18/different-shell-types-interactive-non-interactive-login/
* https://unix.stackexchange.com/questions/38175/difference-between-login-shell-and-non-login-shell
* https://en.wikipedia.org/wiki/Unix_shell
* 

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
* What is Linux Kernel and why it is important
* Kernel Space and User Space
* How Linux works with HW? How to user Kernel Modules
* Linux Boot Sequences
* Systemd Targets (Runlevels)
* Different file types and the File System hierarchy

### Kernel
* Kernel is a major component of the OS and is the interface between computer's HW and the processes running on it.

![alt](./images/os_kernel.png)

* The Kernel is responsible for four major tasks: 
  * Memory Management: Keep track of how much memory is available and how much is used to store what and where
  * Process Management: Determine which processes can use the CPU when and for how long
  * Device Drivers: Acts as in intermediary or interpreter between the HW and the processes
  * System Calls and Security: Receive requests for services from the processes

* The Linux kernel is _monolithic_: This means that the kernel caries out CPU Scheduling, Memory Management, and several other operations by itself
* The kernel is also _modular_: This means it can extend its capabilities through the use of dynamically loaded kernel modules

### Linux Kernel Versions
* Ways to identify Linux kernel versions and understand the naming conventions
* Use the `uname` command to display information about the kernel
  * `uname` simply does not provide much information. It only prints `Linux` meaning the system is using a Linux Kernel
  * Use `uname -r` or `uname -a` flag to provide the print the kernel version, for example `4.15.0-72-generic`. The `4.15.0` is the kernel, major, and minor version; `72` is the patch release or patch level; `generic` is a Distro specific additional Info. 
* The first Linux Kernel was developed by Linus Torvalds in 1991
* The latest release as of this recording is version `5.5.10` release on 18th March 2020
* All Linux distributions make use of any one of these kernel versions, for example Ubuntu 20.04, released in April 2020, uses the Linux kernel version 5 out of the box.
* Check out `http://kernel.org`. This is an open source project that hosts the repositories that make all versions of Linux kernel source code available to all users

### Kernel and User Space
* One of the major responsibilities of Linux Kernel is memory management
* Memory is separated into two areas: Kernel Space and User Space
  * These are synonymous to the terms Kernel Mode and User Mode
  * Kernel space is the portion of the memory in which the Kernel executes and provides its services
  * A process running in the kernel space has unrestricted access to the hardware 
  * Kernel space is strictly reserved to run kernel code, kernel extensions, and most device drivers
  * All process running outside of the kernel reside on the User Space
  * User Space has restricted access to the CPU and the memory

![alt](./images/kernel_and_user_space1.png)  

* Most Unix like Operating Systems, including Linux, come pre-packages with all sorts of programs, such as utilities, programming languages, graphical applications, etc. These are called User Space Applications. This is also often referred to "The User Land"
* Programs in the User Spaces make _system calls_ to the kernel to access hardware, such as memory and the disk. Examples of the system calls are memory allocation or opening a file
  
![alt](./images/kernel_and_user_space2.png)

* Examples of some common system calls to access file system are `open()`, `close()`, `readdir()`, `strlen()`, `closedir()`


## Working with Hardware

* How Linux identifies and manages the HW while it is attached to the system
* List and get detailed information about the devices attached to the system from the command line
* Let's take the example of USB disk attached to the computer
  * As soon as the disk is attached to the system, a corresponding device driver, which is part of the kernel space, detects the state change and generates an event
  * This event, which is called a _uevent_ is then sent to the user space device manager called _udev_
  * The _udev_ service is then responsible for dynamically create a _device node_ associated with the newly attached drive in the `/dev/....` file system
  * When this process is complete, the newly attached disk must be visible under `/dev/...` file system

![alt](./images/hardware_management.png)

* Some ways to list and get detailed information about the HW attached to a Linux system:

* `dmesg` is a tool used to display messages from an area of the kernel called _ring buffer_ 
  * When a Linux OS boots up, there are numerous messages generated by the kernel
  * These messages also contain logs from the HW devices that the kernel detects and provide good indication whether it can configure them
  * You can redirect the output of `dmesg` using `less`, or search for specific keywords using `grep`
  * `dmesg | grep -i usb`

* `udevadm` is the management tool for udevs
  * `udevadm info` command queries the udev database for information about devices.
  * For example `udevadm info --query=pat --name=/dev/sda5` queries a hard disk attached to the system
  * `udevadm monitor` listens to the kernel uevents
  * Upon detecting and event, it prints the details such as the _device pat_ and _device name_ on the screen
  * This command is quite handy to determine the details of a newly attached or removed device
  * Example below shows when a USB mouse is removed from the system

![alt](./images/udevadm.png)

* `lspci` lists and displays information about all the PCI devices connected and configured in the system
  * examples of PCI devices are ethernet cards, video cards, RAID controllers, wireless adapters

* `lsblk` lists information about _block devices_
  * For example below the `sda` is the physical disk; `sda1` to `sda5` are partitions created on this disk
  * In the output of `lsblk`, the TYPE `disk` is the physical disk and the type `part` is a partition
  * Also the `MAJ:MIN` are the major and minor numbers associated with each device. The major number identifies the type of device driver associated with the device. For example number `8` refers to a _block s disk_ device. The minor is used to differentiate between devices that are similar and have the same major number.
  * The table shows some of the commonly used devices along with their major numbers

![alt](./images/lsblk.png)

* `lscpu` displays information about the CPU, such as architecture, socket number, number of cores, threads per core, vendor id, and model name
  * CPU(s) = sockets x cores per socket x threads per core

* `lsmem` list the available memory on the system
  * `lsmem --summary`
* `free -m`  shows the total available vs used memory on the system. `-m` shows the result in MB, `-k` in kB, `-g` in GB

* `lshw` gives detailed information about entire HW configuration on a machine
  * exact memory configuration
  * Firmware version
  * Mainboard configuration
  * CPU version and speed
  * Cache configuration
  * Bus speed
  * and much more
  * `lshw` requires `sudo` to show all information

* with `sudo` you can control which user can run commands as super user; you can also define which commands they can run, and even replay back commands they have run with root privileges.


## Linux Boot Sequence

* Boot processes can be simplified divided into 4 major steps:
  1. BIOS POST
  2. Boot Loader (GRUB 2)
  3. Kernel Initialization
  4. INIT Process, service initialization using _systemd_

* The Linux boot process can be initiated by
  * starting a Linux device that is in _halted_ or stopped state
  * or, by rebooting (aka resetting) the system

* BIOS POST: Is the Power-on Self Test run by BIOS to ensure that device hardware are running correctly. If POST fails the computer may not be operable and the system will proceed to the next step after POST

* After a successful POST, the BIOS loads and executes the boot code from a boot device, which is located at the first sector of the hard disk
  * In Linux, this is located at the `/boot/` file system
  * The boot loader provides the user with the boot screen, often with multiple options to boot into, such as MS Windows or Ubuntu 18.04...
  * Once the user selects an option in the boot screen, the boot loader loads the kernel into the memory, supplies it with some parameters, and hands over the control to the kernel
  * A popular example of a boot loader is GRUB 2, which stands for Grand Unified Bootloader version 2
  * GRUB 2 is the primary boot loader for most current linux distros

* After the selected kernel is loaded into the memory, it is usually decompressed. This is done, as the kernels are usually in a compressed state to save space.
  * The kernel is then loaded into the memory and starts executing
  * During this phase the kernel carries out a series of tasks, such as initializing HW and memory management tasks, ...

* Once the kernel is completely operational
  * it looks for an `init` process to run, which sets up the user space and the processes needed for the user's environment
  * in most of the current day Linux distros, the `init` function then calls the `systemd` daemon
  * the `systemd` is then responsible for bringing the Linux host to a usable state

* `systemd` is responsible for
  * mounting file system
  * starting and managing services
  * it is the universal standard these days
  * but not too long ago, another initialization process called `SystemV` (read System Five, or Sys Five) init was used
  * SystemV was for example used in RHEL 6 or CentOS 6 distros
  * One of the key advantages of using systemd over SystemV is that it reduced system startup time by parallelizing startup of services

* To check which init system is used run
  * `ls -l /sbin/init`
  * it output something like `lrwxrwxrwx   /sbin/init   ->    /lib/systemd/systemd` for systemd
  * basically the `/sbin/init` is a link to the actual init process


## Runlevels

* Linux can run in different modes, such as graphical mode
* You can configure your system to boot into a specific mode
* Modes are set by _Runlevels_

* `runlevel` command shows the current operation mode of the system, for example `3` or `5`
  * Runlevel 5 is the operation mode that provides graphical user interface, runlevel 3 implies a non-graphical mode
  * During boot the init process checks the runlevel and makes sure all the programs that are needed to make the system operational in that mode are started
  * For example the graphical user mode requires a display manager service to run, so that the GUI can work. 

* So a runlevel is basically a name for grouping of the programs that are needed to run for a specific operation mode of the system
* Runlevel were used in SystemV and are not obsolete with systemd. 
* SYSTEMD uses systemd targets instead
* for example the runlevel 3 is called the `multiuser.target` and runlevel 5 is called `graphical.target`
* Look at `man runlevel` for mapping between runlevels and systemd targets

* `systemctl get-default` to get the default systemd target
  * it looks up the file at `/lib/systemd/system/default.target` or `/etc/systemd/system/default.target`
  * which is a link to the default target file, for example `/lib/systemd/system/graphical.target`
  
* `systemctl set-default multi-user.target` changes the default target
  * output: `Created symlink /lib/systemd/system/default.target  -> /lib/systemd/system/multi-user.target`


* https://askubuntu.com/questions/34308/where-is-the-inittab-file
* ![alt](./images/runlevels.png)
* ![alt](./images/runlevel-dirs.png)
* In the runlevel dirs above, programs whose name starts with `S` are run during startup, and programs whose name starts with `K` are run during shutdown (kill); The sequence numbers define the order of running the programs, `S12`, `S50`, `S80`

* The term runlevels is used in the sysV init systems. These have been replaced by systemd targets in systemd based systems. The complete list of runlevels and the corresponding systemd targets can be seen below:
  * runlevel 0 -> poweroff.target 
  * runlevel 1 -> rescue.target
  * runlevel 2 -> multi-user.target
  * runlevel 3 -> multi-user.target
  * runlevel 4 -> multi-user.target
  * runlevel 5 -> graphical.target
  * runlevel 6 -> reboot.target


## File Types
* Everything is a file in Linux
  * i.e. Every object in Linux can be considered to a be a type of file. Even a directory is a special type of file. 

* There are three file types in Linux
  * Regular: normal files, like text, shell scripts, images, etc.
  * Directory: a type of files that contains other files 
  * Special files:
    * Character files: represent the devices under `/dev/` file system. These allow the OS to communicate with IO devices *serially*. Examples include devices such as mouse and keyboard. 
    * Block files: these are files representing *block devices*, also located under `/dev/`. Block devices write and read data from device in blocks (chunks of data), for example hard disk and RAM. `lsblk` lists block devices.
    * Links: links are a way to associate two of more file names to the same file containing data. There are two kinds of links:
      * Hard links: associates two are more file names with the same block of data on the physical disk. Although they behave as independent files, *deleting one link with delete the data*
      * Symbolic links: or symlinks are like pointers to the data in a file. They can be loosely compared to shortcuts in Windows. Deleting a symlink does not delete the data. 
    * Sockets: sockets enable communication between two process
    * Named Pipes: allow connecting one process as an input to another. The dataflow in a pipe is *unidirectional* from the first process to the second. 

* `file` command displays the file type
* `ls -l` also shows the file type as the first letter before permissions: `d`: directory; `-` regular file; `c` character file; `l` link; `s`: socket; `p`: pipe; `b`: block device;


## File System Hierarchy

* `/home`: home dir for all users except the root
* `/root`: home for root
* `/opt`: put any third-party programs here, for example install a web app there
* `/mnt`: mounted file systems using `mount` command
* `/tmp`: temp
* `/media`: all external media (USB disk, external hard disk, etc) are mounted here
  * `df -hP`: disk free, `-h` human readable, `-P` portability POSIX output format; lists information about all mounted file systems
* `/dev`: contains character and block file devices
* `/bin`: contains the basic programs in binary, e.g. `cp`, `mv`, `mkdir`, `date`, ...
* `/etc`: stores most of the configurations
* `/lib` and `/lib64`: shared libraries used by different programs are stored here
* `/usr`: was used for user home directories, but in modern Linux it is the location where all the *user land* applications, libraries, and their data resign. For example, Thunderbird, FireFox, vi, ...
* `/var`: is where the systems writes data of the running systems, such as logs and cached data


# Package Management

## Package Management Introduction

* There are 100s of Linux distros in use today. One of the ways to categorize distros is based on the package manager they use.
  * For example, distros such as RHEL, CentOS, Fedora are based on RPM package manager. They are known as RPM-based distros. RPM packages have the extension `.rpm`
  * Debian, Ubuntu, Arch Linux, Linux Mint, ... use the Debian Package Managers, such as DPKG. Debian packages have the extension `.deb`

* A package is a compressed archive that contains all the files that are required for a software to run
* For example, to instal GIMP (GNU Image Manipulator) on Ubuntu we use the package `gimp.deb`. It contains all the files needed for GIMP to run, such as Application Binaries, Metadata, Configuration files, ...
* You can basically download a package and install it on the Linus using the `.deb` or `.rpm` package file. So why do we need a package manager? 
* A packages manager takes care of all the dependencies of a package and their transitive dependencies and makes sure all the software and dependencies are compatible with the installed Linux distro and version. 
* `dpkg -i gimp.deb` installs GIMP. But it fails if GIMP's dependencies are not installed on the system. 
* A package manager provides a consistent process of installing, configuring, upgrading, and removing packages on a Linux system
* Some of the essential functions of a Package Manager are: 
  * Ensuring the integrity and authenticity of packages, by verifying their digital certificates (digitally signed code) and their checksums. This is to ensure that the package is downloaded from a trusted source and is safe to install
  * Simplified Package Management process: Most Package Mangers provide powerful tools for querying packages in a package repository, downloading, installing, or updating existing software
  * Grouping packages by their function
  * Managing dependencies and avoiding dependency hell

* Different packages managers, depending on distro: 
  * DPKG: (Debian Package) base package manager of Debian-based distros
  * APT: (Advanced Package Tool) a newer frontend for DPKG found in newer distros such as Ubuntu, Linux Mint, Elementary OS, ...
  * APT-GET: traditional frontend for the DPKG in Debian-based distros
  * RPM: (RPM Package Manager, or Red Hat Package Manager) base package manager found in Red Hat-based distributions, such as RHEL, CentOS, Fedora
  * YUM: a frontend for the RPM found in RedHad-based distros
  * DNF: a more feature-rich frontend for the RPM. 


## RPM and YUM

* RPM is used in Red Had-based distros, such as RHEL, CentOS, fedora, ...
* RPM packages have extension `.rpm`
* RPM has five base modes of operations: 
  * Install: `rpm -ivh telnet.rpm`: install a package, `-i` install, `-v` verbose
  * Uninstall: `rpm -e telnet.rpm`
  * Upgrade: `rpm -Uvh telnet.rpm`
  * Query: The RPM database at `/var/lib/rpm` store information about all the packages installed on the system, such as which packages are installed, which version each package is, and any changes to any files after installation. `rpm -q telnet.rpm` queries this database and gives information about a packages
  * Verify: `rpm -Vf <path to file>` verifies a package to make sure it is installed from a trusted and secured source. It compares information about the files installed from package, with the same information from the package metadata
* RPM *does not resolve package dependencies on its own*. That's why we use a higher-level package manager called YUM
  
* YUM (Yellow Dog Updater Modifier) works on RPM-based distros. Talks to RPM software repositories. 
* Repository info is stored at `/etc/yum.repos.d`. Repository files have a `.repo` extension.
* YUM is a high-level package manager that relies on RPM to mange packages
* YUM handles package dependencies unlike RPM
* Software repositories can be local or on the network. Usually the distro comes bundled with its own software repositories, e.g. `/etc/yum.repos.d/redhat.repo`. You can add new repos in `/etc/yum.repos.d` if the software is not found in the official repo, not the lates version, for example `/etc/yum.repos.d/nginx.repo`
* How YUM works: `yum instal httpd`
  * YUM first checks if the package is installed on the system
  * If not, it checks all the configured repos for the availability of package
  * It checks if any dependencies of the software is installed or needs to be upgraded.
  * A *transaction* report is shown to the user to confirm
  * Download and install the necessary `.rpm` packages

* `yum repolist`: show all the repos added to the system
* `yum provides scp`: to check which package to be installed for `scp` command to work
* `yum remove httpd`: remove a package
* `yum update telnet`: update a package
* `yum update`: update all the packages and their dependencies on the system


## DPKG and APT

* DPKG is the base package manager on Debian-based distros (similar to RPM in Red Hat-based distros)
* It can be used to 
  * Install/Upgrade
  * Uninstall
  * List
  * Status
  * Verify
* Debian packages have `.deb` extension
* `dpkg -i telnet.deb` install a package
* `dpkg -r telnet.deb` remove a package
* `dpkg -l telnet` list packages with their version number and short description
* `dpkg -s telnet` to see the status of a package and if it is installed on the system
* `dpkg -p <path to file>` to display information about the package, such as version number, maintainer, ...

* DPKG does not resolve dependencies (similar to RPM). We have to rely on higher-level package managers such as APT or APT-GET
* APT and APT-GET are higher level package managers on Debian-based systems
  * APT (Advanced Package Tool) is more user-friendly and newer that APT-GET
* APT (similar to YUM) relies on software repos for downloading software. Software repos for APT are in `/etc/apt/sources.list`. The repo can be a local one on local file system or on a CD, or it can be remote, accessed over FTP, HTTP, HTTPS
  

* `apt update`: refresh the repos by downloading all package information from all the sources; run it after adding a new repo, or before installing any new package
* `apt upgrade`: upgrade all packages
* `apt edit-sources`: opens up the `/etc/apt/sources.list` in a text editor
* `apt install telnet`: install
* `apt remove telnet`: remove
* `apt search telnet`: look up for a package in the repos
* `apt list | grep telnet`: list all the packages (installed and not installed)

* Difference APT and APT-GET:
  * more user friendly
  * progress bar
  * `apt search search` vs. `apt-cache search telnet`


# Working with Shell II
* Linux is very user friendly; it is just very selective who it is friends with :D 

## File Compression and Archival
* `du`: Disk Usage shows size of files and directories 
* `du -sk`: shows size of file or dir in Kilo Bytes
* `du -sh`: shows the size in human readable format
* `ls -lh`: also shows the human readable size of the file in the listing


* tar (tape archive) creates a single archive of multiple files. Archive files created with TAR are sometimes called tarballs
* `tar -cf test.tar file1 file2 file3` creates an archive of the files. `-c` for create, `-f` for the filename of the archive
* `tar -tf test.tar` list the content of the file. `-t` or `--list`
* `tar -xf test.tar` extracts the archive
* `tar -zcf test.tar file1 file2 file3` creates a compressed (zipped `-z`) archive

* There are different programs for compressing files on the Linux:
  * `bzip2`
  * `gzip`
  * `xz`
* For decompressing:
  * `bunzip2`
  * `gunzip`
  * `unxz`
* For listing the content of the zipped file without decompressing it:
  * `bzcat`
  * `zcat`
  * `xzcat`
* The size of compressed file depends on the type of the data and the compression algorithm


## Searching for files and patterns
* `locate City.txt`  searches for a keyword and returns all paths in the file system with the keyword
  * The downside of `locate` is that it it depends on a database at `/var/lib/mlocate/mlocate.db`
  * the `mlocate.db` is updated once a day by a `cron` job
  * `sudo updatedb` updates the locate database

* `find /home/michael -name City.txt` searches for a file called `City.txt` under the directory `/home/michael`
  * `find` is a very powerful command with many options

* `grep <pattern> <filename>` searches within files for a given pattern
* `grep -i` search case-insensitive
* `grep -r` search recursively within all files in a directory and its subdirectories
* `grep -v` list the opposite. It prints all lines that does not contain the pattern
* `grep -w` search for whole word
* `grep -A<X>` and `grep -B<X>` print X number of lines after or before the line matching the pattern
  * similar to `-context <X>`


## IO Redirection
* In Bash and other Linux shells, when a program is executed, it uses three standard I/O streams. Each stream is represented by a numeric file descriptor:
  * 0 - stdin, the standard input stream.
  * 1 - stdout, the standard output stream.
  * 2 - stderr, the standard error stream.
  * A file descriptor is just a number representing an open file.
* `echo $?` prints the exit code of the program

* With IO Redirection, the standard input, output, and error can be redirected to text files
* `echo $SHELL > shell.txt`. The `>` OVERWRITES the content of the file with the output of the STDOUT of the command
* `echo "hello" >> shell.txt`. The `>>` appends the stdout to the end of file

* To redirect the error messages (stderr) use `2>`
* To suppress the error messages from being displayed on the screen, redirect stderr to /dev/null: `command 2> /dev/null`
* `/dev/null` is Null Device, also called Bitbucket. Everything written to it will be discarded.
* To redirect stderr to stdout and have error messages sent to the same file as standard output, use the following:
  * `command > file 2>&1`
  * `> file` redirect the stdout to `file`, and `2>&1` redirect the stderr to the current location of stdout.
  * The order of redirection is important. For example, `command 2>&1 > file` redirects only stdout to file. This happens because the stderr is redirected to stdout before the stdout was redirected to file.
  * Another way to redirect stderr to stdout is to use the `&>` construct. In Bash `&>` has the same meaning as `2>&1`: 
  * `command &> file` is the same as `command > file 2>&1`

* `grep -r hello /sys/ > /dev/null 2>&1` nothing is printed. stdout is redirected to `/dev/null` and stderr is redirected to stdout. So, everything (stdout, stderr) is sent to `/dev/null`
* `grep -r hello /sys/ &> /dev/null` does the same
* to see the exit code of the program use `echo $?`

* A Pipe `command1 | command2` makes the stdout of the `command1` to be the stdin of `command2`
* `tee` The tee command reads from the standard input and writes to both standard output and one or more files at the same time. tee is mostly used in combination with other commands through piping.
* `command | tee file1.out file2.out file3.out` write the output of the command to stdout and also the the files
* `tee -a` appends the file instead of overwriting
* `tee` is handy in combination with `sudo`
  * `sudo echo "newline" > /etc/file.conf` does not work, because the redirection is not run by `sudo` but with the unprivileged user. It will result in `bash: /etc/file.conf: Permission denied`
  * `echo "newline" | sudo tee -a /etc/file.conf` will do the work

* https://www.cs.ait.ac.th/~on/O/oreilly/unix/upt/ch08_19.htm
* https://unix.stackexchange.com/questions/159513/what-are-the-shells-control-and-redirection-operators

* https://www.cs.ait.ac.th/~on/O/oreilly/unix/upt/ch08_19.htm


## VI Editor
* Using `cat > blah.txt` we can start typing and into file `blah.txt`. Pressing `CTRL-D` (EOT, End-of-Transmission) writes the typed text into file. 

* `vi <filename>`
* vi Operation Modes:
  * Command mode: give commands to the editor, such as copy, paste, delete, navigate between lines, ... Press `Esc` to go to command mode from other modes
  * Insert mode: lets you enter text. Press `i`, `a`, `o`, `I`, `A`, `O` (each doing a different thing)  to go insert mode. 
  * Last line mode: commands to save changes, discard changes, exit, ... Press `:` to go to Las line mode
  * default mode is command mode

* Command mode: 
  * `k j l h` to move the cursor
  * `v` for highlighting in visual mode
  * `yy` copy (yank) line
  * `p` paste
  * `ZZ` save the file
  * `x` delete the letter at cursor
  * `dd` delete line
  * `dNd` delete N lines from current line
  * `u` undo
  * `r` redo
  * `/` find text downward, press `n` next down, `N` next up, `?` search upward (revers)

* Insert mode: 
  * `i`, `a` insert text before, after cursor
  * `I`, `A` insert in the line before, after cursor
  * `o`, `O` insert new line before, after cursor

* Last line (commend line) mode:
  * `:` activate command line mode
  * `:w` save teh file
  * `:q` exit
  * `:wq` write and quit
  * `:q!` quit without saving

* VIM: Vi Improved is a newer more feature rich version of vi
  * in most distros the command `vi` is a symlink to `vim`


# Security and File Permissions

* Basic security and identifying file types
* Creating users and groups
* Managing file permissions and ownerships
* Special directories and files

![alt](./images/security_in_linux.png)

* Security in Linux includes many aspects, amongst others:
  * Access Control
  * PAM: Pluggable Authentication ModulesLinux Pluggable Authentication Modules (PAM) is a suite of libraries that allows a Linux system administrator to configure methods to authenticate users. It provides a flexible and centralized way to switch authentication methods for secured applications by using configuration files instead of changing application code.[1] There are Linux PAM libraries allowing authentication using methods such as local passwords, LDAP, or fingerprint readers.[2] Linux PAM is evolved from the Unix Pluggable Authentication Modules architecture. Linux-PAM separates the tasks of authentication into four independent management groups:
    * account modules check that the specified account is a valid authentication target under current conditions. This may include conditions like account expiration, time of day, and that the user has access to the requested service.
    * authentication modules verify the user's identity, for example by requesting and checking a password or other secret. They may also pass authentication information on to other systems like a keyring.
    * password modules are responsible for updating passwords, and are generally coupled to modules employed in the authentication step. They may also be used to enforce strong passwords.
    * session modules define actions that are performed at the beginning and end of sessions. A session starts after the user has successfully authenticated.
    * https://en.wikipedia.org/wiki/Linux_PAM
  * Network Security: Mostly using Firewall rules, IP Tables, ...
  * SSH Hardening: Make sure only authorized users have remote access to a Linux system
  * SELinux: Security-Enhanced Linux (SELinux) is a Linux kernel security module that provides a mechanism for supporting access control security policies, including mandatory access controls (MAC). SELinux is a set of kernel modifications and user-space tools that have been added to various Linux distributions. Its architecture strives to separate enforcement of security decisions from the security policy, and streamlines the amount of software involved with security policy enforcement. The key concepts underlying SELinux can be traced to several earlier projects by the United States National Security Agency (NSA).

## Linux Accounts
* Every user has an account in Linux:
  * User account maintains the information such as username and password used to login to the system
  * A user account contains an identifier called **UID**, which is unique for each user
  * Information about user accounts is stored in `/etc/passwd` file

* A group is a collection of users; it is used to organize users based on common attributes such as role or function
  * Information about groups is stored in `/etc/group` file
  * Each group has a unique identifier called **GID**
  * Groups can be used to grant access to files and directories to a group of users

* A user account contains:
  * username
  * UID, user ID
  * GID, the ID of the group the user is part of. Each user is member of a default group with the same ID as the UID (a group with the same name as username). It is assigned if no group is defined for the user when it is created. This is the primary GID of the user. A user can be member of multiple groups. 
  * information about user's home dir e.g. `/home/<username>`
  * default shell for the user, e.g. `/bin/sh`

* `id` command prints information about the user: uid, gid, groups
* `grep -i <username> /etc/passwd` prints the entry of the user in the `/etc/passwd` file, showing username, uid, gid, home dir, default shell, ...

![alt](./images/user_account.png)

* There are other types of accounts apart from normal users:
  * super user account: root, uid=0; Root has unrestricted access to everything on the system
  * system accounts: created when the OS is installed, and are used by the programs and software that is not supposed to run as root. Examples are ssh, mail,... These accounts have uid below 100 or between 500 to 1000; They normally don't have a home directory, of if they have, it is not under `/home`
  * service accounts: are similar to system accounts and are created when services are installed, such as nginx, mercury, ...
  
![alt](./image/../images/account_types.png)

* Commands to see information about users:
  * `id`: shows information about a user
  * `who`: shows a list of users currently logged in to the system
  * `last`: shows a record of all logged in users, and date and time the system was last rebooted

![alt](./images/id_who_last.png)

* Switching user:
  * `sudo`: run programs with the security privileges of another user, by default the superuser.
  * `su`: switch to any other user, e.g `su jane` and enter jane's password. When used with a hyphen e.g. (`su - jane`) it can be used to start a login shell. In this mode users can assume the user environment of the target user. `su -` login as root
  * `su -c <username>` The meaning of “command” is slightly different: for `su -c`, it's a string that's executed by the target user's shell, whereas for `sudo` with no options, it's a program to run with arguments. But for common usage, they're the same.
  * https://askubuntu.com/questions/620936/difference-between-su-and-sudo-su
  * https://askubuntu.com/questions/70534/what-are-the-differences-between-su-sudo-s-sudo-i-sudo-su
  * https://askubuntu.com/questions/331062/what-is-the-functional-difference-between-sudo-su-and-sudo-i
  * https://unix.stackexchange.com/questions/16334/what-is-the-difference-between-sudo-and-su-c

* `shopt`: This builtin allows you to change additional shell optional behavior.

* sudo:
  * `/etc/sudoers`: defines the policy used by the `sudo` command
  * `visudo` update the `/etc/sudoers` command
  * only users listed in the `/etc/sudoers` can use `sudo` for privilege escalation
  * using `/etc/sudoers` users can be granular privileges to use `sudo`, for example which command can a user run using sudo
  * the syntax of the `/etc/sudoers` file: user or group, e.g. root, or %admin; hosts; as-user:as-group; command. In all cases ALL means no restriction

* Using `sudo` we can eliminate the need to ever login as root
  * by setting `/usr/sbin/nologin` as the default shell for the root user


## User Management


## Access Control Files


## File Permissions and Ownership


## SSH and SCP


## Introduction to IPTABLES Rules


## Securing the Environment


## Cron Jobs


# Networking

## DNS

## Networking Basics


## Troubleshooting



# Storage in Linux


## Disks and Partitions


## File System in Linux


## DAS NAS and SAN


## NFS


## LVM



# Service Management with SYSTEMD

## Creating a SYSTEMD service


## SYSTEMD Tools
