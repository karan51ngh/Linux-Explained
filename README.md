# Linux-Explained

- Welcome to **Linux-Explained** – a beginner-friendly guide to understanding and using Linux.
- This repository is designed to help new users, tech enthusiasts, and aspiring developers get comfortable with the Linux operating system. 
- Whether you're switching from another OS, learning Linux for development, or just curious about how it works, this guide aims to simplify the core concepts and tools.
- The goal is to offer a straightforward, beginner-friendly reference to help you build a strong foundation in Linux.

## Index of Content:
- [Introduction to Linux](#a-brief-introduction-to-linux)
    - [What is GNU](#what-is-gnu)
- [Linux File System](#linux-file-system)
    - [Linux Filesystem Hierarchy Structure](#linux-filesystem-hierarchy-structure)
    - [About various directories](#about-various-directories)
    - [File System Navigation using CLI](#file-system-navigation-using-cli)
    - [`pwd`](#pwd), [`ls`](#ls), [`cd`](#cd), [`touch`](#touch), [`cat`](#cat), [`mv`](#mv), [`cp`](#cp), [`rm`](#rm), [`rmdir`](#rmdir)
- [Package Managers](#package-managers)
    - [Introduction to Package Managers](#introduction-to-package-managers)
    - [Package Managers and Software Packages](#from-where-do-package-managers-get-these-software-packages)
    - [View List of Repositories](#how-to-check-the-list-of-repositories-your-system-accesses-for-installing-software)
    - [`apt` package manager](#apt-package-manager)
    - [`dpkg` package manager](#dpkg-package-manager)
    - [`apt` vs `dpkg`](#apt-vs-dpkg)
- [File Permissions](#file-permissions)
    - [Types of Permissions and Users](#types-of-permissions-and-users)
    - [Working with Permissions](#working-with-permissions)
    - [chmod](#chmod-command-is-used-for-modifying-the-permissions-of-a-filedirectory)
- [Process Management](#process-management)
    - [`top`](#top), [`kill`](#kill), [`killall`](#killall)

## A Brief Introduction to Linux

- Linux is an open-source operating system kernel created by [Linus Torvalds](https://github.com/torvalds) in 1991.
- Together, [GNU](#what-is-gnu) and Linux (also called GNU/Linux) form a complete operating system, often just called Linux.
- The GNU Project provided all the essential tools needed to make a complete, usable operating system.
- Linux is a Unix-like system, meaning it's inspired by the design of Unix. Unix was a closed-source operating system developed in the 1970s at AT&T’s Bell Labs.

- #### What is GNU
    - GNU stands for “GNU’s Not Unix” – a recursive acronym.
    - It’s a free software project started by Richard Stallman in 1983.
    - It's  Goal: Create a completely free and open Unix-like operating system.
    - GNU is a collection of free software tools (created by the Free Software Foundation) that work with the Linux kernel to form a full operating system.
    - Since Unix was proprietary, GNU set out to recreate it with open-source alternatives:

        | **Component**     | **GNU Replacement**                                       |
        |-------------------|-----------------------------------------------------------|
        | Shell             | GNU Bash - `bash` (Bourne Again Shell)                    |
        | System libraries  | GNU C Library - `glibc`                                   |
        | File utilities    | coreutils - [ls](#ls), [cp](#cp), [echo](#echo) etc.      |
        | Compiler          | GNU Compiler Collection - `gcc`                           |
        | Debugger          | GNU Debugger - `gdb`                                      |
        | Build tools       | `make`, `autoconf`, etc.                                  |
        | Bootloader        | `GRUB` (GRand Unified Bootloader)                         |
- In 1991, Linus Torvalds released the Linux kernel. Combining GNU tools + Linux kernel = a working operating system → GNU/Linux.

## LINUX FILE SYSTEM

- A file system in an operating system (OS) is a way of organizing and storing data on storage devices like hard drives, SSDs, USB drives, etc. 
- It defines how files are named, stored, retrieved, and managed.
- The Linux file system is a **hierarchical directory structure** that organizes files and directories in a **tree-like** structure, with a single **root** directory at the top of the hierarchy, represented by  `/`. 
- Below the root directory, there are a number of other directories, including `/bin`, `/dev`, `/etc`, `/home`, `/lib`, `/mnt`, `/proc`, `/sbin`, `/tmp`, and `/usr`.
- In Linux, **Everything is a File**. For example, devices, sockets, and even processes are treated as files, enabling uniform interaction via standard I/O operations.
- Each file has access [permissions](#file-permissions) (*read*, *write*, *execute*) for *owner*, *group*, and *others*, controlled via commands like [chmod](#chmod), [chown](#chown), and [chgrp](#chgro).
- External filesystems (like USBs or other partitions) are integrated into the directory tree using the [mount](#mount) command at specific mount points.

### Linux Filesystem Hierarchy Structure

```bash
/                       # Root directory (top-level of the filesystem)
├── bin/                # Essential user binaries (e.g., ls, bash)
├── boot/               # Boot loader files (e.g., kernel, initrd)
├── dev/                # Device files (e.g., /dev/sda)
├── etc/                # System-wide configuration files
├── home/               # Home directories for users
│   ├── karan51ngh/     # Personal directory for a user named karan51ngh
│   └── torvalds/       # Personal directory for a user named  torvalds
├── lib/                # Essential shared libraries
├── media/              # Mount point for removable media (e.g., USB drives)
├── mnt/                # Temporary mount point for filesystems
├── opt/                # Optional application software packages
├── proc/               # Virtual filesystem for process and kernel info
├── root/               # Home directory for the root user
├── run/                # Temporary runtime files
├── sbin/               # System binaries (usually for root)
├── srv/                # Data for services provided by the system
├── sys/                # Virtual filesystem for system and device info
├── tmp/                # Temporary files (often cleared on reboot)
├── usr/                # Secondary hierarchy for read-only user data
│   ├── bin/            # Non-essential user binaries
│   ├── lib/            # Non-essential libraries
│   └── share/          # Architecture-independent data
└── var/                # Variable data (e.g., logs, spool files)
```
### About various directories

 - `/` : This is the root directory and the starting point of the file system. All other directories are contained within it.
 - `/bin` : This directory contains executable programs (also known as Binaries) that are essential for system operation, such as [ls](#ls), [cp](#cp), [mv](#mv), [mount](#mount), [rm](#rm), etc.
 - `/boot` : This directory contains the files needed for booting the system, including the kernel and bootloader.
 - `/dev` : This directory contains device files, which are used to communicate with hardware devices such as printers and USB drives.
 - `/etc` : This directory contains system configuration files, such as the configuration files for the network, user accounts, and startup scripts.
 - `/home` : This directory contains user home directories, where users can store their personal files.
 - `/lib` : This directory contains shared library files that are used by the system and applications.
 - `/media` : This directory is used for mounting removable media such as CDs, DVDs, and USB drives.
 - `/mnt` : This directory is used for temporarily mounting file systems, such as network file systems or external hard drives.
 - `/opt` : This directory is used for installing optional software packages.
 - `/proc` : This directory provides information about the running processes and system resources.
 - `/root` : This directory is the home directory for the root user.
 - `/sbin` : This directory contains essential system administration programs, such as init and shutdown that generally can only be employed by the [superuser]().
 - `/srv` : can contain data directories of services such as HTTP (/srv/www/) or FTP.
 - `/sys` : is a virtual filesystem that can be accessed to set or obtain information about the kernel's view of the system.
 - `/tmp` : This directory is used for temporary files that are created by the system and applications.
 - `/usr` : This directory contains non-essential system files, such as user programs and documentation.
 - `/var` : This directory contains variable data files, such as log files and spool directories.
 
### File System Navigation using CLI.

File system navigation in Linux can be done using the command line interface.
Here are the commands needed in brief:

- ##### `pwd` 
	>This command in Linux stands for **"print working directory"**. It is used to display the current working directory, which is the directory that the user is currently in.

- ##### `ls`
	>This command in Linux is used to list the contents of a directory and it also provides information about the files and directories in the current directory / specified directory.

    - *Syntax*: `ls [options] <DIRECTORY_NAME>`. `<DIRECTORY_NAME>` by default is the current working directory. 
    - *options*:
        - `ls`: Shows files and directories in short format.
        - `ls -a`: Shows **hidden** (that start with a dot `.`)files and directories. 
        - `ls -l` / `ll`: Shows **detailed information** about each file and directory, including the file permissions, ownership, size, and modification date.
        - `ls -h`: Shows file sizes in a **human-readable format**, such as "*2.3K*" or "*4.5M*".
        - `ls -t`: Sorts files and directories by **modification time**, with the most recently modified files and directories listed first.
        - `ls -r`: **Reverses** the **order** of sort, so that files and directories are listed in reverse order.
        - `ls -S`: **Sorts** files by size, with the largest files listed first.
        - `ls -R`: Lists the contents of subdirectories **recursively**.
        - `ls --color`: Adds **color** to the **output**, making it easier to read.
- ##### `cd` 
    >This command in Linux is used to change the current working directory.

    - *Options*:
        - `cd` / `cd ~`: Changes the current working directory to your **home** directory.
        - `cd <DIRECTORY_NAME>`: Changes the current working directory to the specified directory.
        - `cd -`: Changes the current working directory to the **previous** working directory.
        - `cd ..`: Changes the current working directory to the **parent** directory.
- ##### `touch`
	>This command in Linux is used to create an empty file or update the timestamp of an existing file.

    - *Syntax*: `touch [OPTION]... <FILE_NAMES>...`
    - *Options*:
        - `touch <file_name>`: Creates an empty file with the specified name, or updates the timestamp of an existing file.
        - `touch -a <file_name>`: Updates only the **access time** of the specified file.
        - `touch -m <file_name>`: Updates only the **modification time** of the specified file.
        - `touch -d [date] <file_name>`: Sets the access and modification times of the specified file to the specified date and time. The date must be in the format **YYYY-MM-DD HH:MM:SS**.
- ##### `cat`
	>This command is primarily used to concatenate and display the contents of one or more files, but can also be used to modify them.

    - *Syntax*: `cat [OPTION]... <FILE_NAMES>...`
    - *Options*:
        - `cat <file_name>`: Displays the contents of the specified file on the screen.
        - `cat <file_1> <file_2>`: **Concatenates** the contents of two or more files and displays them on the screen.
        - `cat -n <file_name>`: Displays the contents of the specified file on the screen, with line numbers.
        - `cat -b <file_name>`: Displays the contents of the specified file on the screen, with line numbers only for non-blank lines.
        - `cat <file_1> >> <file_2>`: **Appends** contents of *file_1* to the contents of *file_2*.
        - `cat <file_1> > <file_2>`:  **Replaces** the contents of an *file_2* with the content of *file_1*.
- ##### `mv`
	>This command is used to move or rename files and directories.

    - *Syntax*: `mv [Options] [source/directory/FILE_NAME] [destination/directory/FILE_NAME]`
	- *Options*:
	    - `mv file.txt /home/user/new_directory/`: move the file file.txt to the directory /home/user/new_directory/.
		- `mv -i <file_name> <directory_name>`: Makes the process **interactive**, **prompts** before overwriting an existing file.
		- `mv -f <file_name> <directory_name>`: **Forces** the move or rename operation without prompting, even if the destination file already exists.
		- `mv -v <file_name> <directory_name>`: Displays **verbose** output, showing the names of the files or directories being moved or renamed.
		- `mv <file_1> <file_2>`: This will **rename** the file from *file_1* to *file_2*.
- ##### `cp`
	>This is used to copy files and directories from one location to another.

    - *Syntax*: `cp [Options] [source/directory/file/name] [destination/directory/file/name]`
	- *Options*:
	    - `cp <file_1> /home/user/new_directory/`: copy the file *file_1* to the directory */home/user/new_directory/*.
		- `cp -i <file_name> <directory_name>`: Makes the process **interactive**, **prompts** before overwriting an existing file
		- `cp -f <file_name> <directory_name>`: **Forces** the copy operation without prompting, even if the destination file, with the same name already exists.
		- `cp <file_1> <file_2> <file_3> /destination/directory`: 
		Copying **multiple files**.
		- `cp -r /home/user/old_directory /home/user/new_directory/`: This will **recursively copy** the **directory** */home/user/old_directory* and its contents to the directory */home/user/new_directory/*.
		- `cp <file_1> <file_2>`: This will create a copy of the file *file_1* to the same directory, with the name *file_2*.
- ##### `rm`
	>This is used to remove or delete files and directories.

    - *Syntax*: `cat [OPTION]... <FILE_NAMES> <DIR_NAMES>...`
    - *Options*: 
        - `rm <file_1>`: This will delete file_1.
        - `rm -r <directory_name/>`: This will recursively delete the directory directory and its contents.
        - `rm -f <file_1>`: *Forces** the deletion of file without prompting, even if the file is write-protected.
        - `rm -i <file_1>`: Makes the process **interactive**, **prompts** before deleting the file
- ##### `rmdir`
	>This command is used to remove empty directories in Linux.
   	
    - *Syntax*: `rmdir <directory_name>`

## PACKAGE MANAGERS

### Introduction to Package Managers:

- **Package managers** are software tools for *installing*, *updating*, and *removing software packages* on a computer system.
- They maintain a **database** of available **software packages** and their **dependencies**.
- Package managers automatically download and install necessary dependencies when a user requests the installation or removal of a package.
- Package managers also provide features for managing *package updates*, such as checking for *new versions* and *installing security patches*.
- Popular package managers include *apt*, *dpkg*, *yum*, *rpm*, *pacman*.

### From where do Package Managers get these Software Packages:

- Package managers obtain software packages from **software repositories**.
- Repositories are typically hosted on servers that are accessible over the internet. 
- Repositories can be maintained by the operating system vendor, a third-party provider, or the community.
- Package managers connect to the appropriate repository and download the necessary packages and dependencies.
- This ensures that the packages are obtained from a **trusted source** and are the correct version for the system.
- Popular repositories include Ubuntu's official repositories, Arch Linux's AUR, and Red Hat's EPEL repository.
- Package managers, such as `apt` and `yum`, are used to interact with repositories and download and install packages from them.

### How to check the list of repositories your system accesses for installing software:

Here Terminal Commands for checking the repositories on various major Linux distributions:
- For **Debian** or **Ubuntu**:
    - ` sudo nano /etc/apt/sources.list`
    - This command will open the sources.list file in a text editor.
- For **Fedora** or **CentOS**:
    - `sudo yum repolist`
    - This command will display the repository IDs and names for all enabled repositories on your system.
    - To view more detailed information about a specific repository `sudo yum info <repository-name>`
- For **Arch Linux**:
    - `cat /etc/pacman.conf`
    - This command will display the contents of the configuration file for the Pacman package manager.

### apt package manager

- The `apt` command is a package management tool for **Debian-based** Linux distributions.
- *Syntax*: `apt [options] <package_name>`
- *Options*:
    - `apt update`: updates the package lists from the repositories.
    - `apt upgrade`: upgrades the installed packages to their latest versions.
    - `apt install package`: installs the specified package and its dependencies.
    - `apt remove package`: removes the specified package, but leaves its configuration files intact.
    - `apt purge package`: removes the specified package along with its configuration files.
    - `apt autoremove`: removes any unused dependencies that were installed as a result of package  - installations or removals.
    - `apt search package`: searches for packages with the specified name or keywords.
    - `apt show package`: displays detailed information about the specified package.
    - `apt list`: lists all installed packages on the system.
        - `apt list --installed`: To see all the installed packages on the system.
        - `apt list --upgradable`:  To see all the packages that have a newer version ready to be upgraded.
    - ` apt dist-upgrade`: Upgrade all installed packages, including those that require the installation of new dependencies or the removal of existing ones.
    - `--fix-broken`: Attempt to fix broken dependencies when installing a package.
    - `apt edit-sources`: opens the sources.list file for editing.
- You can use apt to install a .deb file by  `sudo apt-get install /path/to/package.deb`. When using apt to install a .deb file, the package manager will not automatically resolve dependencies or install any required dependencies.
- If you want to use apt to install a .deb file and automatically resolve dependencies, use: `sudo apt --fix-broken install /path/to/package.deb`
- the `--fix-broken` option is specific to the `apt` command and is not supported by the `dpkg` command. `dpkg` is a **lower-level** package manager that works with individual `.deb` packages. It does not have the ability to automatically resolve dependencies or install packages from a remote repository.
- Examples:
    - To update the package lists, run: `sudo apt update`
    - To install the 'htop' package, run: `sudo apt install htop`
    - To remove the 'thunderbird' package, run: `sudo apt remove thunderbird`
    - To search for packages containing the word 'editor', run: `sudo apt search editor`
    - To list all installed packages on the system, run: `sudo apt list`
 
### dpkg package manager:
 
- `dpkg` is a package manager for **Debian-based** systems such as **Ubuntu**. It is used to *install*, *remove*, and *manage software packages* in the `.deb` format.
- *Syntax*: `dpkg [options] <package_name.deb>`
- *Options*:
    - `-i`/`--install`: Install a package from a .deb file.
    - `-r`/`--remove`: Remove a package from the system, leaving its configuration files intact.
    - `-P`/`--purge`: Purge a package from the system, and remove the package and its configuration files.
    - `--unpack`: Unpack a package, but do not configure it.
    - `--configure`: Configure an unpacked package.
    - `--force-depends`: Force the installation of a package even if it depends on a package that is not installed.
    - `--force-remove-reinstreq`: Force the removal of a package even if it is required by other installed packages.
    - `list`: List the installed packages on the system.
    - `search`: Search for a package by name.
    - For a complete list of options, `--help` flag with the `dpkg` command.
- dpkg installs packages on Ubuntu in order to follow the Filesystem Hierarchy Standard (FHS), which defines a standard directory structure for Unix-like operating systems.
- When you use dpkg to install a package, the package and its files are installed in the following locations:
    - **Executable files**: `/usr/bin`
    - **Libraries**: `/usr/lib`
    - **Documentation**: `/usr/share/doc`
    - **Configuration files**: `/etc`
- Examples:
    - Install a package: `sudo dpkg -i /path/to/package.deb`
    - Uninstall a package: `sudo dpkg -r package_name`
    - Purge a package: `sudo dpkg -P package_name`
    - List all installed packages: `dpkg --list`
    - Show details about a package: `dpkg --status package_name`
    - Query which package a file belongs to: `dpkg --search file_path`
    - Extract files from a package: `dpkg -x package_name.deb directory_path`

### Differences between `apt` and `dpkg` package managers
 
 - `dpkg` and `apt` are both package managers for Debian-based systems such as Ubuntu.
 - `dpkg` is a lower-level package manager that works with **individual .deb packages**. 
 - **`dpkg` does not have the ability to automatically resolve dependencies or install packages from a remote repository.**
 - `apt` is a higher-level package manager that is built on top of `dpkg`. It has the ability to automatically resolve dependencies and install packages from a remote repository, making it easier to use than dpkg.
 
## FILE PERMISSIONS

>File permissions are a way of controlling access to files and directories. 

### Types of Permissions and Users

>There are **three types of permissions**: *read*, *write*, and *execute*.

- **Read (r)** - The read permission allows a user to **view** the contents of a file or directory. When applied to a directory, it allows the user to see the names of the files and subdirectories within it.
- **Write (w)** - The write permission allows a user to **modify** the contents of a file or directory. When applied to a directory, it allows the user to create, delete, or rename files and subdirectories within it.
- **Execute (x)** - The execute permission allows a user to **run** a program or script. When applied to a directory, it allows the user to access the files and subdirectories within it.

>These permissions are assigned to **three categories of users**: *owner*, *group*, and *others*.

- **owner** is the user who **created** it or the user who currently owns it. 
- **group** is a collection of users who share **similar permissions** to access certain files or directories. You can give multiple users the same level of access to that file or directory without having to set individual permissions for each user
- **others** includes all users who do not fall into the categories of owner or group.

### Working with Permissions
- To view the file permissions, use `ls -l` command:
    
    *output*:
    
    ```bash
    -rwxrw-r-- 12 karan51ngh users 64.0K Feb  26 11:11 file_name
    |[-][-][-]-   [--------] [---]
    | |  |  | |      |       |
    | |  |  | |      |       +-------------> 7. Group Name
    | |  |  | |      +---------------------> 6. Owner Name
    | |  |  | +----------------------------> 5. Alternate Access Method
    | |  |  +------------------------------> 4. Others Permissions
    | |  +---------------------------------> 3. Group Permissions
    | +------------------------------------> 2. Owner Permissions
    +--------------------------------------> 1. File Type
    ```
- The table below represents what **number is assigned** for all the different **types of permissions**.
    | Number | Permission Type        | Symbol      |
    | ------ | ---------------------- | ----------- |
    | 0      | Permission Type        | ---         |
    | 1      | Execute                | --x         |
    | 2      | Write                  | -w-         |
    | 3      | Execute + Write        | -wx         |
    | 4      | Read                   | r--         |
    | 5      | Read + Execute         | r-x         |
    | 6      | Read + Write           | rw-         |
    | 7      | Read + Write + Execute | rwx         |
    
- ##### `chmod` 
    >This is used for modifying the permissions of a file/directory.
    
    - *Symbollic mode*:
        - *Syntax*: `chmod <user_type><take/remove permission><list_of_permissions> <file_names>`
        - *Examples*:
            - to add execute permissions for the owner of a file you would run: `chmod u+x file_name`
            - to add read and write permissions for the group that owns the file, you would run: `chmod g+rw file_name`
            - to remove write permissions for the owner of a file you would run: `chmod o-w file_name`
    - *Numeric Mode*:
        > We can use the numbers(from the above table) assigned to different permissions.
        
        - *Syntax*: `chmod <number_owner><number_group><number_others> <file_names>`
        - *Example*:
            - to set permissions on a file to rwxrw-r-–, you would run: `chmod 764 file_name`

## Process Management

A process is an instance of a running program, and each process has its own unique process ID (**PID**), as well as other attributes such as a parent process ID (**PPID**), priority(**PR**), CPU and memory usage, and input/output streams.

- ##### `top`
    >This is used to monitor the performance of the system and display real-time information about the processes running on it.
    
    - *Syntax*: `top [options]`
    - *Options*:
        - `top -d <n>`: sets the delay as *n seconds* between updates of the process list.
        - `top -n <n>`: sets the number of iterations for which the `top` command will run before exiting as *n*.
        - `top -p <process_id1>,<process_id2>,...`: allows you to specify the process ID(s) to monitor.
        - `top -u <user_name>`: allows you to filter the output by the speified user.
        - `top -H`: displays the process hierarchy in a tree-like format. This is useful for understanding the relationships between processes.
        - `top -o <field_name>`:allows you to sort the output by a specific field. For example `top -o %CPU`, `top -o TIME`, `top -o UID`, `top -o %MEM` etc.
        
- ##### `kill`
    >The is used to send     signals to running processes. The signals can be used to control the behavior of the processes or terminate them.
    
    - *Syntax*: `kill [signal] [pid]`
    - *Signals*:
        - **TERM** (signal 15): Request that the process terminate gracefully.
        - **KILL** (signal 9): Forcefully terminate the process without allowing it to perform any cleanup.
        - **HUP** (signal 1): Send the hangup signal, which is typically used to request that a process reload its configuration file.
        - **INT** (signal 2): Send the interrupt signal, which is similar to pressing Ctrl+C on the keyboard.
        - If you **do not specify** a signal, kill sends the **TERM signal by default**, which requests that the process terminate gracefully.
        - use the `-s` option to specify a signal by name rather than number. For example, `kill -s SIGTERM [pid]` is equivalent to `kill -15 [pid]`.
    - *Examples*:
        - `kill 1234`: Send the default TERM signal to the process with the ID 1234.
        - `kill -9 5678`: Forcefully terminate the process with the ID 5678 using the KILL signal.
        - `kill -s HUP 9876`: Send the hangup signal to the process with the ID 9876.
        - `kill -INT 2345`: Send the interrupt signal (equivalent to Ctrl+C) to the process with the ID 2345.
    
- ##### `killall`
    > This command is used to send signals to all processes that match a given name, making it a more convenient way than `kill` to terminate multiple processes at once. By default, killall sends the TERM signal.
    
    - *Syntax*: `killall [options] <name>`
    - *Options*:
        - `killall -u <user> <name>`: Send the default TERM signal to all <name> processes owned by the user <user>.
        - `killall -g <group> <name>`: Send the default TERM signal to all <name> processes belonging to the users group <group>.
        - `-v` and `-i` are used for verbose output and interactive process respectively.
    - *Examples*:
        - `killall firefox`: Send the default TERM signal to all processes with the name firefox.
        - `killall -s KILL apache2`: Forcefully terminate all processes with the name apache2 using the KILL signal.
        - `killall -i -s TERM sshd`: Interactively prompt the user before sending the TERM signal to all sshd processes.
        - `killall -u alice firefox`: Send the default TERM signal to all firefox processes owned by the user alice.
        - `killall -g users chrome`: Send the default TERM signal to all chrome processes belonging to the users group.