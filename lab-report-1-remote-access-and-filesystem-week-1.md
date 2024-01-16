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
The current directory before using the `cd` command was `/home/lecture1`, this is shown by the using `pwd` command which prints the current working directory. If we use the `cd` command with no arguments, it will take you to the `HOME` directory. The `cd` command changes the current working directory to the given argument or path. Since no argument was given, it takes us back to the start or the `/home` directory. This is not an error.


2. `cd` used with a path to a directory as an argument
```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
If we use the `cd` command with the argument, `lecture1/`, it will take us to that path or directory. Previously, we were in the `/home` directory but using the `cd` command we were able to switch into the directory given. This did not result in an error and if we use the `pwd` command we can see that we were taken to `/home/lecture1` which shows `cd` ran successfully.

3. `cd` used with a path to a file as an argument
```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
[user@sahara ~/lecture1]$ cd Hello.java 
bash: cd: Hello.java: Not a directory
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
In the `/home/lecture1` directory, if we use the `cd` command with a path to the file, `Hello.java`, it prints `Not a directory`. This is because we cannot change the directory to a file. This results in an error since the `cd` command was not able to change directories and stayed in `/home/lecture1` seen through the `pwd` command.

# `ls`
1. `ls` used with no arguments
```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ ls
lecture1
```
The `ls` command prints the files and folders in the given path. In the `/home` directory, if we use the `ls` command with no arguments it will list the files and folders in the current directory. Since we are currently in the `/home` directory it lists the files and folders in the `/home` directory and in this case the only thing listed was the folder `lecture1`. This did not result in an error.

2. `ls` used with a path to a directory as an argument
```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ ls lecture1/
Hello.class  Hello.java  messages  README
[user@sahara ~]$ pwd
/home
```
In this case, we are still in the `/home` directory. But, if we use `lecture1/` as an argument, we can view the files and folders within that directory without changing directories. We can see this by using the command `pwd` which shows that we did not change directories. This did not result in an error. 

3. `ls` used with a path to a file as an argument
```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
[user@sahara ~/lecture1]$ ls Hello.java 
Hello.java
```
While in the `/lecture1` directory, we can try using the `ls` command with a path to the file `Hello.java`. This does not result in an error but instead just lists the file since there are no files or folders within the `Hello.java` file.


# `cat`
1. `cat` used with no arguments
```
[user@sahara ~]$ cat
Concatenate this text 
Concatenate this text
```
In this we are trying to use the command `cat` while in the `/home` directory with no arguments. The `cat` command usually displays the contents of one or more files. Since we did not include any path to a file, it reads the user's input and reprints the input. This is not an error but shows the behavior of the `cat` command which reprints whatever you input whether that is a file or user input.

2. `cat` used with a path to a directory as an argument
```
[user@sahara ~]$ cat lecture1/
cat: lecture1: Is a directory
```
In the current path `/home`, if we input the path `lecture1` as an argument, it will result in an error. It displays that the path we input `Is a directory`. The `cat` command can only print the contents of files and not folders/directories. 

3. `cat used with path to a file as an argument
```
[user@sahara ~/lecture1/messages]$ pwd
/home/lecture1/messages
[user@sahara ~/lecture1/messages]$ cat en-us.txt 
Hello World!
```
In the `/home/lecture1/messages` directory, if we use the `cat` command with the path to the file `en-us.txt` as an argument, it will print the contents of the file which was `Hello World!`. This is not an error. 



