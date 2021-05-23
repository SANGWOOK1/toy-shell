# toy-shell
project #1 homework(Shell)

-> Coded on Ubuntu 20.04  
-> 'host name' and ' user name' colors are Blue("\033 34m") and CYAN("\033 35m")  
-> exit[0] and [1] will exit in Myshell   
-> and support command line arguments  
-> uses cd(chdir), pwd, ls, mkdir for this shell  

# Support command line arguments

1. mkdir -> create new directory (ex. -p dirname/subdname)
2. touch -> It plays the role of randomly changing the date of an existing file. 
The timestamp change is mainly used to compile source files or to determine the point of random access. 
It also plays a role of creating an empty file with no contents if the file does not exist.
(ex. filename, -c filename)

3. cp -> command for copy files (ex. cp abc.txt newabc.txt , cp abc.txt sub.abc.txt)
4. rm -> It is used to delete files and directories, and file recovery is not possible or file recovery is very difficult.
(ex. rm -r dir/, rm -rf dir/)
5. ls -> Check the contents of the directory.
(ex. ls -a, ls -s, ls -r, ls -h, ls -u,-c, ls -lu, ls -lc)
