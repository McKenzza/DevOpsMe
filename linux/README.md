# Linux Base Commands

## Contents
- [**Basic Commands**](#basic-commands)
- [**Info Commands**](#info-commands)


## Basic Commands
### Where am I?

How to understand where we are? For this we have `pwd` command, which <b>p</b>rints current <b>w</b>orking <b>d</b>irectory:
```bash
$ pwd
/home/user
```
We are in user's home directory! Cool.

### Which files are located in some directory?

To answer this question, we have `ls` command, which <b>l</b>i<b>s</b>ts directory contents of files and directories:

```bash
$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
```

Next usage with the key `[-a]` prints all the files with hidden files and directories that will be denoted as . at the start of the file or directory names:

```bash
$ ls -a
. .. .bash_history .bash_history Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
```
Next case - prints as a list `[-l]` or we can use alias `ll`
```bash
$ ls -l # ll
total 32
drwxr-xr-x  2 user    user   4096 Mar 15 15:33 Desktop
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Documents
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Downloads
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Music
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Pictures
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Public
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Templates
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Videos
```

we can combine the keys `ls -al`
```bash
$ ls -al
total 32
drwx------ 39 user    user   4096 Mar 24 13:52 .
drwxr-xr-x  4 root    root   4096 Mar 13 19:25 ..
-rw-------  1 user    user     22 Mar 24 11:05 .bash_history
-rw-r--r--  1 user    user    220 Mar 10 18:10 .bash_logout
-rw-r--r--  1 user    user   5551 Mar 10 18:10 .bashrc
drwxr-xr-x  2 user    user   4096 Mar 15 15:33 Desktop
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Documents
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Downloads
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Music
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Pictures
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Public
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Templates
drwxr-xr-x  2 user    user   4096 Mar 13 19:30 Videos
```

where
|Name|Description|
|---|---------------|
|.| current directory|
|..| parent directory|
|.\<filename\>| hidden files|
|\<filename\>| regular files|

and finally we can print specific directory content `ll [dir]`:
```bash
$ ll Downloads/
total 0
```
but we have no files here.

## Info commands

### Who am I? Really.

Just enter `whoami` command

```bash
$ whoami
user
```

### How long server is up?

Command [uptime](## "Gives a one line display of the following information: the current time, how long the system has been running, how many users are currently logged on, and the system load averages for the past 1, 5, and 15 minutes") tells us how long the system running:

```bash
$ uptime
 16:49:56 up  8:34,  1 user,  load average: 1.02, 0.94, 0.89
```

or in pretty format

```bash
$ uptime -p
up 8 hours, 34 minutes
```

### Who is logged on?

Command `w` displays information about currently logged in users and what each user is doing. The header shows the same information like [uptime](#how-long-server-is-up) command

```bash
$ w
 17:20:49 up  9:05,  1 user,  load average: 0.55, 0.58, 0.67
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
user     tty1     -                08:16    9:05m  0.16s  0.16s /usr/bin/process
```
