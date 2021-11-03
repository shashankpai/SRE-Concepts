
# Mastering the Command line 

When learning linux and working on linux systems mastering command line is very important skillset a good SRE should have , Here we have a collection of command 
line tips and useful info to master for SRE's

These fe exercises and tricks will help junior SRES to master the trade and become efficient with command line


# 1. What is a shell 
```
When we speak of the command line, we
are really referring to the shell. The shell is
a program that takes keyboard commands
and passes them to the operating system to
carry out. Almost all Linux distributions supply a shell
program from the GNU Project called bash. The name
is an acronym for bourne-again shell, a reference to the
fact that bash is an enhanced replacement for sh, the
original Unix shell program written by Steve Bourne
```

# 2. Some Simple Commands

# date
```
$ date
Wed Nov  3 09:16:31 UTC 2021
```

# cal

```
A related command is cal, which, by default, displays a calendar of the
current month.
```
```
$ cal
   November 2021      
Su Mo Tu We Th Fr Sa  
    1  2  3  4  5  6  
 7  8  9 10 11 12 13  
14 15 16 17 18 19 20  
21 22 23 24 25 26 27  
28 29 30              
```

# df 

`To see the current amount of free space on our disk drives, enter df.`

```
$ df
Filesystem     1K-blocks      Used Available Use% Mounted on
udev             1764564         0   1764564   0% /dev
tmpfs             357928      1100    356828   1% /run
/dev/sda1       41020640  30359740   8547468  79% /
tmpfs            1789636         0   1789636   0% /dev/shm
tmpfs               5120         4      5116   1% /run/lock
tmpfs            1789636         0   1789636   0% /sys/fs/cgroup
SharedData     494465020 183069444 311395576  38% /home/shashank/Desktop/SharedData
SharedData     494465020 183069444 311395576  38% /media/sf_SharedData
tmpfs             357924        16    357908   1% /run/user/1000
```

# Ending a terminal session

We can end a terminal session by closing the terminal emulator window, by
entering the exit command at the shell prompt, or by pressing ctrl-D.

`$ exit`


