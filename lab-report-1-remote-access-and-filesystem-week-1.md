# Lab Report 1 - Remote Access and FileSystem 

# `cd`
1. `cd` used with no arguments
```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
[user@sahara ~/lecture1]$ cd
[user@sahara ~]$ pwd
/home
```
The current directory before using the `cd` command was `/home/lecture1`, this is shown by the using `pwd` command which prints the current working directory. If we use the `cd` command with no arguments, it will take you to the `HOME` directory. The `cd` command changes the current working directory to the given argument or path. Since no arugment was given, it takes us back the start or the `/home` directory. This is not an error.


2. `cd` used with a path to a directory as an argument
```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
If we use the `cd` command with the argument, `lecture1/`, it will take us to that path or directory. Previously, we were in the `/home` directory but used the `cd` we are able to switch into the directory given. This did not result in an error since if we use the `pwd` command we can see that we were taken to `/home/lecture1`.

3. `cd` used with a path to a file as an argument
```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
[user@sahara ~/lecture1]$ cd Hello.java 
bash: cd: Hello.java: Not a directory
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
In the `/home/lecture1` directory, if we use the `cd` command with a path to the file, `Hello.java`, it prints `Not a directory`. This is because we cannot change the directory to a file. This results in an error since the `cd` command was not able to change directorys and stayed in `/home/lecture1` seen through the `pwd` command.

# `ls`
1. `ls` used with no arguments
```
[user@sahara ~]$ ls
lecture1
```
The `ls` command lists the available files and folders in the current working path. `ls` listed the folder `lecture1` as it is the only file/folder accessable for the `HOME` directory. 

2. `ls` used with path to a directory as an argument
```
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
```
The current directory was `/home` but using a directory as an argument we are able to see the files accessible in the `/lecture1` path. 
3. `ls` used with path to a file as argument
```
[user@sahara ~/lecture1]$ ls Hello.java
Hello.java
```
While in the `/lecture1` directory, if we use a file as an argument, the `ls` command just returns the file since it is the only thing accesible unlike if it was a folder with other accesible files.

# `cat`
1. `cat` used with no arguments
```
[user@sahara ~]$ cat
Concatenate this text 
Concatenate this text
```
`cat` used with no argument will take the user input and duplicate it. For instance, I had input "Concatenate this text" and it printed our that input. `cat` usually takes one or more agrs and concatenates the files.

2. `cat` used with path to a directory as an argrument
```
[user@sahara ~]$ cat lecture1
cat: lecture1: Is a directory
```
In the current path `/home`, if we input a directory as a argument, it will result in an error and with be unable to concatenate as the `cat` prints the contents of files and is unable to with a directory. 

3. `cat used with path to a file as an argument
```
[user@sahara ~/lecture1/messages]$ cat en-us.txt 
Hello World!
```
In the `/lecture1/messages` directory, using the file, `en-us.txt`, as an argument will print the contents of the file.



