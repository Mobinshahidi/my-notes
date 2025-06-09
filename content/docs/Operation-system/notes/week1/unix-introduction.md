---
title: unix introduction
description: unix introduction
---

# UNIX introduction
- unix operation system is made up of three parts;
	1. the kernel
		the kernel of unix is the hub of os: it allocates time and memory to programs and handles the file store and communications in response to system calls
	2. the shell
	   the shell acts ad an interface between the user and the kernel. when a user logs in, the login program checks the username and password, and then start another program called the shell. the shell is a command line interpreter (cli). it interprets the commands the user types in and arranges for them to be carried out. the commands are themselves programs: when they terminate, the shell gives the user another prompt(% on our systems)
	3. the programs

> [!NOTE] important
> **everything in unix is either a file or a process.** 

- process is an executing program identified by a unique pid(process identifier).
- a file is a collection of data. they are created by users using text editors, running compilers etc.
- all the files are grouped together in the directory structure. the file-system is arranged in a hierarchical structure, like an inverted tree. the top of the hierarchy is traditionally called root.                        ![[IMG-20250410180722739.png]]
  - In naming files, characters with special meanings such as **/ * & %** , should be avoided. Also, avoid using spaces within names. The safest way to name a file is to use only alphanumeric characters, that is, letters and numbers, together with _ (underscore) and . (dot).

 - File names conventionally start with a lower-case letter, and may end with a dot followed by a group of letters indicating the contents of the file. For example, all files consisting of C code may be named with the ending .c, for example, prog1.c . Then in order to list all files containing C code in your home directory, you need only type ls *.c in that directory.

- **Beware**: some applications give the same name to all the output files they generate.    
	For example, some compilers, unless given the appropriate option, produce compiled files named **a.out**. Should you forget to use that option, you are advised to rename the compiled file immediately, otherwise the next such file will overwrite it and it will be lost.
### **important commands :**

| command                 | detail                                                                                                                          |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| ls                      | The ls command lists the contents of your current working directory.                                                            |
| ls -a                   | To list all files in your home directory including those whose names begin with a dot, type                                     |
| mkdir                   | to make a directory                                                                                                             |
| cd                      | to change directory to another directory(just cd move us to home directory)                                                     |
| cd .                    | stays in the current directory                                                                                                  |
| cd ..                   | will take you one directory up the hierarchy                                                                                    |
| pwd                     | print working directory path                                                                                                    |
| cp file1 file2          | copy file1 and call it file2                                                                                                    |
| mv file1 file2          | move or rename file1 to file2                                                                                                   |
| rm file                 | remove a file                                                                                                                   |
| rmdir directory         | remove a directory                                                                                                              |
| cat file                | display a file                                                                                                                  |
| cat                     | reads the standard input (the keyboard), and on receiving the'end of file' (^D), copies it to the standard output (the screen). |
| more file               | display a file a page at a time                                                                                                 |
| head file               | display the first few lines of a file                                                                                           |
| tail file               | display the last few lines of a file                                                                                            |
| grep 'keyword' file     | search a file for keywords(case sensitive)                                                                                      |
| grep -i                 | ignore case sensitive                                                                                                           |
| wc file                 | count number of lines/words/characters in file                                                                                  |
| command > file          | redirect standard output to a file                                                                                              |
| command >> file         | append standard output to a file                                                                                                |
| command < file          | redirect standard input from a file                                                                                             |
| command1 \| command2    | pipe the output of command1 to the input of command2                                                                            |
| cat file1 file2 > file0 | concatenate file1 and file2 to file0                                                                                            |
| sort                    | sort data                                                                                                                       |
| who                     | list users currently logged in                                                                                                  |
| a2ps -Pprinter textfile | print text file to named printer                                                                                                |
| lpr -Pprinter psfile    | print postscript file to named printer                                                                                          |
| *                       | match any number of characters                                                                                                  |
| ?                       | match one character                                                                                                             |
| man command             | read the online manual page for a command                                                                                       |
| whatis command          | brief description of a command                                                                                                  |
|apropos keyword         | match commands with keyword in their man pages |
| diff filename1 filename2| compares files, and shows where they differ|
|chmod options filename  | lets you change the read, write, and execute permissions on your files. The default is that only you can look at them and change them, but you may sometimes want to change these permissions. For example, **chmod o+r _filename_** will make the file readable for everyone, and **chmod o-r _filename_** will make it unreadable for others again. Note that for someone to be able to actually look at the file the directories it is in need to be at least executable. See [help protection](http://www-csli.stanford.edu/Help/.help/intro-computer/protection) for more details.|
|ff                      | finding files|
