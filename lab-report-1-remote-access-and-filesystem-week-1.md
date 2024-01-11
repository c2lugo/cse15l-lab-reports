# Lab Report 1 - Remote Access and FileSystem 

`cd`
1. `cd` used with no arguments
```
[user@sahara ~]$ cd
[user@sahara ~]$ 
```
The `cd` command is used to switch the current directory to the given path(arg). Since no arg is given, cd takes us to the `HOME` directory. Furthermore the directory in this case is `/home`. This did not result in an error.

2. `cd` used with path to directory as argument
```
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$
```
In this `cd` switched the current directory to the given path with was `lecture1`. This did not result in an error and if we take a look at the commmand line we can see our current directory is `/lecture1`.

3. `cd` used with a path to a file as argument
```
[user@sahara ~/lecture1]$ cd Hello.class
bash: cd: Hello.class: Not a directory
```
This results in an error. The `cd` command only takes given directorys as an argument. If we give a file is will print that `Not a directory`. The current directory stayed in `/lecture` since the `cd` command was unable to switch into a file.

`ls`
1. `ls` used with no arguments
```
[user@sahara ~]$ ls
lecture1
```
This `ls` command lists the available files and folders in the current working path. `ls` listed the folder `lecture1` as it is the only file/folder accessable for the `HOME` directory. 

2. `ls` used with path to directory as argument
```
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
```
The current directory was `/home` but using a directory as an argument we are able to see the files accessible in the `/lecture1` path. 
