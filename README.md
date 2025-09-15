# learn-linux
This repo is used as a notes that I make following along the course 'Hands-on Introduction to Linux Commands and Shell Scripting' on Coursera.

## Module 1 - Introduction to Linux
### Linux Distribution
* A specific flavor of linux OS also referred to as Distro
* Linux kernel is the core component
* There are hundred of distros

Linux distro differences
* system utilities
* GUI is different
* each of them use different shell commands
* support types:
  * community vs enterprise
  * Long-term support (LTS) vs rolling release

Linux Distros:
- Debian - largest
- Ubuntu - derived from Debian
- Red Hat Linux
- Fedora
- SUSE Linux Enterprise
- Arch Linux

### Overview of Linux Architechture
Five layers of Linux:
- UI
  Allows user ot interact user with machine
- APPLICATION
  any software that lets you perform task
  - System daemons
  - shells
  - user apps
  - tools
- OPERATING SYSTEM
  controls the jobs and programs
- KERNEL  
  performs vital operations, lowest level software, starts on boot, bridge between apps and hardware  
  Key Jobs:
  - Memory management
  - process management
  - device drivers
  - security
- HARDWARE

Linux filesystem:
- collection of files in your machien
- Begin at root directory (/)
- Tree-like structure

`/` :
  - `/bin`
  - `/usr`
  - `/home`
  - `/boot`
  - `/media`
  - ...

### Linux Terminal Overview
what is linux shell
what is linux terminal
how linux terminal and shell work together
how to use linux terminal to navigate directories

- the shell is OS-level application that interprets commands
  - You can use GUI but shell is still used
- use commands to:
  - move and copy files
  - write to and read from files
  - extract and filter data
  - search for data
- Shells:
  - Bash
  - Zsh

- We interact shell with **terminal**
- enter commands and receive output from them

__How command runs?__  
`User` ---> `Terminal` --->  `Shell OS Kernel` ---> `Hardware`  
Then it return to user.  

Paths in linux filesystem:  
- ex: `/home/me/Documents/`
- __'a/b'__ indicates file or directory named b inside parent directory a
- Special paths:
  - `~` Home directory
  - `/` Root directory
  - `..` Parent of current directory

**Changing the current working directory:**
```
/home $ cd /
/ $ cd bin
/bin $ ./ls
---[lists of all items inside bin]---
/bin $
/bin $ cd ~ ###___navigate to home___###
/home/me $
```

```
/home $ cd .. ###___navigates to parent___###
/ $ cd /media/my-usb-drive
/media/my-usb-drive $ cd ../../home/me/Documents   ###___moves to media to root then to home to me to Documents___###
/home/me/Documents $ cd ..
/home/me $ python ./myprogram.py  ###___starts python and runs myprogram.py in the current directory___###
Hello, World!  ###___returned message to the terminal window___###
/home/me $
```

btw, `$` <--- this is called command prompt  
about `pwd` and `ls` commands:  
btw, `pwd` stands for present working directory and it print the path name to the present working directory  
also, note that the return output is printed as text by default
```
/home/project $ pwd
/home/project
/home/project $ ls
/home/project $ ls /home  ###___can list contents of any directory by specifying the directory name___###
project  theia
/home/project $ ls /  ### ___`/` is the root directory of which entire filesystem branches out___###
bin  dev  home  lib32  libx32  mnt  proc  run  srv  tmp  var  boot  etc  lib  lib64  media  opt  root  sbin  sys  usr
/home/project $ 
```

**Terminal Tips:**
- Tab completion: press `tab` and it autocompletes the directory name
- Command History: navigate to previous commands using `Up Arrow` and `Down Arrow` keys

**BAM BAM INFO:**
- if you type `ls /bin` you will so many files and one of the files is `ls`
- when you enter `ls` command, Linux searches for and runs the `ls` command by executing the binary file `/bin/ls`

## Creating and Editing Text Files
__Popular text editors__:
- Command-line text editors:
  - GNU Nano
  - vi
  - vim
- GUI-based text editors:
  - gedit
- Command-line or GUI:
  - emacs

Features of gedit:  
comes preinstalled on most linux distros  
uses syntax color coding  
easy to use with clean, simple gui:
- Integrated file browser
- undo and redo
- search and replace
- extensibility

Features of GNU nano:  
- undo and redo
- search and replace
- syntax highlighting
- indenting groups of lines
- line numbers
- line-by-line scrolling
- multiple buffers

To open a file in GNU nano from the command prompt, type:  
`nano <filename>`

File editing with vim:  
To start vim, type: `vim`  
To specify a file to edit, type: `vim <filename>`  
Two basic modes:
- __Insert__ and __Command__
  
__Insert mode__:
- Press _i_ to enter Insert mode
- Type some text
- press Esc to exit insert mode and switch to command mode
- the text is written to the buffer at the cursor location
  
__Command mode__:
- Enter: `:sav example.txt` to create a file and write the buffer to the file
- Enter `:w` to write the buffer to the file without exiting
- Enter `:q` to quit vim session
- Enter `:q!` to quit without saving

___lab learnings___:
- `sudo` "super-user do"
- `apt` "advanced packaging tool". use it to perform system administration operations such as installing software packages, upgrading existing packages, and updating your system's package list index
```
commands used:
sudo apt update    ---to ensure all package dependencies are up-to-date---
sudo apt upgrade nano    ---to upgrade nano to latest supported version of nano---
sudo apt install vim    ---as vim isn't preinstalled in linux---

---to create a new file with nano---
nano hello_world.txt
ctrl + x to exit nano
cat hello_world.txt    ---it printed the content of text file---

---vim---
vim    ---start vim---
:q    ---to exit---
vim hello_world2.txt    ---to create and edit using vim---
press _i_ to enter insert mode
press _esc_ to exit insert and enter command mode
:w    ---to save the work, this writes the contents of text buffer to your text file---

---bash---
created a file done.txt
type echo "done with lab!"
bash done.txt
```

## Installing software and updates
__Packages and package managers__:
- Packages:
  - Archive files
  - For installing new software or updating existing software
- Pacakge managers:
  - Manage the download and installation of packages
  - available for different linux distros
  - can be GUI-based or command-line tools

__Deb and RPM packages__:
- Packages for linux OS
- Distinct file types for different linux OS
- .deb files:
  - for debian-based distributions such as Debian, Ubuntu, and Mint
  - deb stands for Debian
- .rpm files:
  - For Red Hat-based distributions such as CentOS/RHEL, Fedora and openSUSE
  - RPM stands for Red Hat Package Manager
- deb and RPM formats are equivalent
- If a package is only available in onoe format, you can use alien to convert it:
  - RPM to deb:  
    `alien <package-name> .rpm`
  - deb to RPM:
    `alien -r <package-name> .deb

Updating deb-based linux  
GUI tool: __Update Manager__  
Command line: __apt__

Updating RPM-based linux  
GUI tool: __PackageKit__  
Command line: __yum__

Installing new software  
deb package with apt:  
 `sudo apt install <package-name>`  
rpm package with yum:  
 `sudo yum install <package-name>`  

Other software package managers:  
- python package managers include pip and conda
- Installing the pandas library:  
  `pip install pandas`

## Module 2 - Introduction to Linux Commands

### Overview of common Linux Shell Commands
What is a shell?  
- user interface for running commands
- interactive language
- Scripting language

- Default shell is usually Bash
- other shells include sh, ksh, tcsh, zsh, and fish

```
$ printenv SHELL  ###___To know what's the default___###
/bin/bash
$ bash
```

__Shell command applications__:
- getting information
- navigating and working with files and directories
- printing file and string contents
- compression and archiving
- performing network operations
- monitoring performance and status
- running batch jobs

__Getting information__:
- `whoami` - username
- `id` - user ID and group ID
- `uname` - operating system name
- `ps` - running processes
- `top` - resource usage
- `df` - mounted file systems
- `man` - reference manual
- `date` - today's date

__Working with files__:
- `cp` - copy file
- `mv` - change file name or path
- `rm` - remove file
- `touch` - create empty file, update file timestamp
- `chmod` - change/modify file permissions
- `wc` - get count of lines, words, characters in file
- `grep` - return lines in file matching pattern

__Navigating and working with directories__:
- `ls` - list files and directories
- `find` - find files and directory tree
- `pwd` - get present working directory
- `mkdir` - make directory
- `cd` - change directory
- `rmdir` - remove directory

__Printing file and string contents__:
- `cat` - print file contents
- `more` - print file contents page-by-page
- `head` - print first N lines of file
- `tail` - print last N lines of file
- `echo` - print string or variable value

__Compression and archiving__:
- `tar` - archive a set of files
- `zip` - compress a set of files
- `unzip` - extract files from a compressed zip archive

__Networking__:
- `hostname` - print hostname
- `ping` - send packets to URL and print response
- `ifconfig` - display or configure system network interfaces
- `curl` - display contents of file at a URL
- `wget` - download a file from URL

__Running Linux on a Windows machine__:
- Dual boot with a partition
- Install Linux on a virtual machine
- Use a Linux emulator
- Windows Subsystem for Linux (WSL)

### Informational Commands
__User information__:
- Display user information
- verify identity or indentify user account
- `whoami` - return user name
- `id`(identity) - user or group ID
- ```
  $ whoami
  johndoe
  $ id -u
  501
  $ id -u -n
  johndoe
  ```

__System information__:
`uname` (Unix name) - returns OS information
- Identify system or diagnose issues
```
$ uname
Darwin
$ uname -s -r  ###___return os name and version___###
Darwin 20.6.0
$ uname -v
......more info.......
```

__Displaying your disk usage__:
`df`(disk free) - Shows disk usage
- Monitor disk usage or check space
```
$ df -h ~
...
$ df -h   ### for each file###
```

__Displaying current running process__:
`ps` (process status) - Running processes
- Monitor or manage processes
```
$ ps -e  ### displays any current process regardless of users ###
...
```

__Monitoring system health and status__:
`top` (table of processes) - Task manager
- Monitor system performance and resource usage
```
$ top -n 3
```

__Printing strings and variable values__:
`echo` - Print string variable value
```
$ echo  ### empty line ###

$ echo Hello
Hello
$ echo "Learning Linux is fun!"  ### good practice to write in quotes ###
Learning Linux is fun!
$ echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

__Getting date information__:
`date` - Displays system date and time
```
$ date
Mon Sep 15 00:20:57 IST 2025
$ date "+%j day of %Y"
258 day of 2025
$ date "+It's %A, the %j day of %Y"
It's Monday, the 258 day of 2025
```
| Specifier | Explanation |
| --------- | ----------- |
| `%d` | Displays the day of the month (01 to 31) |
| `%h` | Displays the abbreviated month name (Jan to Dec) |
| `%m` | Displays the month of the year (01 to 12) |
| `%Y` | Displays the four-digit year |
| `%T` | Displays the time in 24 hour format as HH:MM:SS |
| `%H` | Displays the hour |

__Viewing the manual__:
`man` (manual) - Shows manual for any command
```
$ man id
...
```

```
### can use tldr command, why? more accessible than man ###
npm install -g tldr

tldr command_name
```

### File and Directory navigation commands
listing directory content:
`ls`(list) - list files and directories
```
$ ls
Desktop		Downloads	Movies		Pictures Documents	Library		Music		Public
$ ls Downloads
...contents of Downloads...
$ ls -l
...more information version...
```
`pwd` - finding current working directory  
`cd`(change directory) - change directory  
`find` - find files in directory tree
 - ```
   $ pwd
   /Users/me/Documents
   $ find . -name "a.txt"
   ./folder1/a.txt
   $ find . -iname "a.txt"
   ./folder1/a.txt
   ./folder2/A.txt
   ```
### File and Directory management commands
+ `mkdir`(make directory)  
+ `rm`(remove) - remove file or directory  
  - `rm -r <folder-name>` - to remove a directory
  - `rmdir <folder_name>` - if the directory is made using mkdir (recommended)  
+ `touch` - create empty file, update file date  
+ `cp`(copy) - copy file or directory to destination
  - `cp /source/file /dest/filename` - to copy files
  - `cp -r /source/dir /dest/dir` to copy directories  
+ `mv`(move) - move file or directory
  - `mv /source/file /dest/dir` - for files
  - `mv /source/dir /dest/dir` for directories  
+ `chmod`(change mode) - change file permissions
  - ```
    $ ls -l my_script.sh
    -rw-r- -r- my_script.sh  ### read write permissions ###
    $ ./my_script.sh
    bash: permission denied ./my_script.sh
    $ chmod +x my_script.sh
    # ls -l
    -rwxr-xr-x my_script.sh
    $ ./my_script.sh
    Learning Linux is fun!
    ```

 __BAM BAM__:
 - `*` is a special character called wildcard. It is used to represent any string of characters
   + `ls /bin/b*` lists all files starting with b
   + `ls /bin/*r` lists all files ending with r
 - common options to try with `ls` command:
   | Option | Description |
   | ------ | ----------- |
   | `-a` | list all files, including hidden files |
   | `-d` | list directories only, do not include files |
   | `-h` | with `-l` and `-s`, print sizes like 1K, 234M, 2G |
   | `-l` | include attributes like permissions, owner, size and last-modified date |
   | `-s` | sort by file size, largest first |
   | `-t` | sort by last-modified date, newest first |
   | `r` | reverse the sort order |


### Security: managing file permissions and ownership
```
$ echo 'who can read this file?' > my_new_file
$ more my_new_file
who can read this file?
$ ls -l my_new_file
-rw-r--r-- 1 theia users ...
```
- in `-rw-r--r--` the first `-` represents that the permissions are referring to a file, for a directory it would be `d`
- first three characters `rw-` define users permission, next three `r--` group, and the final three `r--` other
- `rw-` means read, write but not execute(x)
- __for directory__:
  | directory permission | permissible actions(s) |
  | `r` | list directory contents using `ls` command |
  | `w` | add or remove files or directories |
  | `x` | enter directory using `cd` command |
  | `s` | special permission |

__Making a file private__:
```
chmod go-r my_new_file
ls -l my_new_file
-rw------- 1 theia users ...
```
removing for group and others, the read permission.

### Viewing file content
`cat`(catenate) - print entire file contents  
`more` - print file contents page-by-page  
`head` - print first N lines of file (default 10)  
`tail` - print last N lines  
`wc`(word count) - Count characters, word, lines
```
$ ls
numbers.txt
$ cat numbers.txt
...100 to 1...  ### takes entire command line ###
$ more numbers.txt
...press [space] to change page and exit with [q]...
$ head numbers.txt
...0 to 9...
$ head -n 3 numbers.txt
... 0 to 2...
$ cat pets.txt
... cat cat cat cat dog dog cat...
$ wc pets.txt
7 7 28 pets.txt  ### 7 lines 7 words 28 characters, it counts \n as well ###
$ wc -l pets.txt
7 pets.txt
$ wc -w pets.txt
7 pets.txt
$ wc -c pets.txt
28 pets.txt
```

### Commands for wrangling text files
`sort` - sort lines in a file
`uniq`("unique") - Filter out repeated lines
`grep`("global regular expression print") - Return lines in file matching pattern
`cut` - Extracts a section from each line
`paste` - Merge lines from different lines
```
$ sort pets.txt
... cat cat cat cat cat dog dog ...
$ sort -r pets.txt
... dog dog cat cat cat cat cat ...
$ uniq pets.txt
... cat dog cat ...
$ cat people.txt
... name of people ...
$ grep ch people.txt
Dennis Ritchie
Erwin Schrodinger
$ grep -i ch people.txt  ### case insensitive ###
Charles Babbage
Dennis Ritchie
Erwin Schrodinger
$ cut -c 2-9 people.txt
...lan Turi ...
$ cut -d ' ' -f2 people.txt  ### delimiter ' ' and field 2 that is last names of people ###
... Turing Stroustrup ...
### let's say we have three files first.txt last.txt yob.txt ###
$ paste first.txt last.txt yob.txt
... looks like table, uses \t as the default delimitter ...
$ paste -d "," first.txt last.txt yob.txt
Dennis,Ritchie,1921
```

