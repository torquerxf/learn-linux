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



