---
layout: post
title:      "Linux Basics (Shell Commands)"
date:       2020-09-24 05:39:40 +0000
permalink:  linux_basics_shell_commands
---


## About Linux
Linux was created by a Software Engineer named [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds). Linux is a *"family of open source Unix-like operating systems based on the [ Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel)" - [Wikipedia](https://en.wikipedia.org/wiki/Linux)*. The first Linux kernal was written in 1991. The Software layers used to describe the Linux structure are as follows:<br>
**.** **The kernal** - Runs the hardware and allocates resources. <br>
**.** **The shell** (Which I will focus on here) - Where you type commands into the CLI (Command Line Interface).<br>
**.** **Applications layer** - Where programs run, such as [gcc](https://en.wikipedia.org/wiki/GNU_Compiler_Collection) (Gnu Compiler Collection) and [vi](https://en.wikipedia.org/wiki/Vi) (a popular text editor).<br>
<br>
*Linux Operating System hierarchy*
<iframe src="https://drive.google.com/file/d/1aZG_XBPWyeievIo9g-IgUAbYVgnFcAuY/preview" width="640" height="480"></iframe>


## Linux file system

In Most operating systems including Linux, directories (aka. folders) are structured in a hierarchical tree like way. This keeps our files and folders organized. The root directory is labeled as a  forward slash '/' character, all other directories sit below the root. When you first login you will be taken to the home directory.


*Linux file system tree*
<iframe src="https://drive.google.com/file/d/1XqVALdF3_a8S6vO70VZ9465nBQf1lChM/preview" width="640" height="480"></iframe>


## Basic commands
The following is a list of some of the most common Linux shell commands *(each command will be followed by `/$ ` which is just an example of being in the root directory of the terminal)*:<br>

`/$ ls` - List storage. This command will list the contents of the current directory you're in.<br>
`/$ cd` - Change directory. This will bring you to your home directrory. To navigate up a level use `cd..`, back a directory `cd -`, to root `cd /`, or if you have it follow a path it will bring you to that directory, for example ` cd home/jay/documents`.<br>
`/$ pwd` - Print working directory. Outputs the path of the current working directory starting from the root. Example `/home/jay/photos`.<br>
`/$ mkdir` - Make directory. Short for make directrory, will create a new directory when followed up with a name that the user types (must be all lower case), for example `mkdir myfiles`.<br>
`/$ touch` - Mainly used to create new empty files `touch myfile`.<br>
`/$ rm` - Remove. This command is mainly used for removing files and directories. Use this with caution as there is no trash bin in Linux.<br>
`/$ mv` - Move. Moves file(s) from one directory to another `mv file1.txt file2.txt`, also can be used to rename a file `mv name newname`.<br>
`/$ echo` - Outputs lines the user types in front of it as string arguments `echo "Hello World!"`. This command is usually used in shell scripts and batch files.<br>
`/$ grep` - Global Regualr Expression Print. My favorite, this is a very useful command that can be used to search for string charcaters in a file. When it finds the characters you're searching for it will output the result `grep "hello" greeting.txt`.


*Linux video resources: [Linux: a short documentary](https://www.youtube.com/watch?v=aurDHyL7bTA&feature=emb_title), [What is Linux](https://www.youtube.com/watch?v=zA3vmx0GaO8)*
