# Linux Base Commands

## Contents

- [**Basic**](#basic)
  - [Where am I](#where-am-i)
  - [How long server is up](#how-long-server-is-up)
  - [Manuals](#manuals)
- [**User Info**](#user-info)
  - [Who am I](#who-am-i)
  - [Who is logged in](#who-is-logged-in)
- [**File Management**](#file-management)
  - [Which files are located in some directory](#which-files-are-located-in-some-directory)
  - [How to create a file](#how-create-a-file)
  - [How to remove a file](#how-to-remove-a-file)
  - [How to read a file](#how-to-read-a-file)
  - [Determine file type](#determine-file-type)
  - [Copy file](#copy-file)
  - [How to rename file](#how-to-rename-a-file)

## Basic

### Where am I

How to understand where we are? For this we have `pwd` command, which **p**rints current **w**orking **d**irectory:

```bash
$ pwd
/home/user
```

We are in user's home directory! Cool.

### How long server is up

Command `uptime` (Gives a one line display of the following information: the current time, how long the system has been running, how many users are currently logged on, and the system load averages for the past 1, 5, and 15 minutes) tells us how long the system running:

```bash
$ uptime
 16:49:56 up  8:34,  1 user,  load average: 1.02, 0.94, 0.89
```

or in pretty format

```bash
$ uptime -p
up 8 hours, 34 minutes
```

### Manuals

Command `man` prints the system reference manuals

```bash
man pwd
```

Also you can use `info` command for view documentation

```bash
info uptime
```

## User Info

### Who am I

Just enter `whoami` command

```bash
$ whoami
user
```

Command `groups` prints the groups a user is in

```bash
$ groups
user adm dialout cdrom floppy sudo audio dip video plugdev users netdev wireshark bluetooth lpadmin kaboxer docker
```

Command `id` prints real and effective user and group IDs

```bash
$ id
uid=1000(user) gid=1000(user) groups=1000(user),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),100(users),101(netdev),113(wireshark),116(bluetooth),121(lpadmin),132(kaboxer),986(docker)
```

### Who is logged in

Command `who` shows information about currently logged in user.

```bash
$ who
user  tty1         2024-03-24 08:16
user  pts/0        2024-03-24 08:16 (:1)
user  pts/1        2024-03-24 08:19 (:1)
```

|Subject|Description|
|---|----------------|
|user | login name|
|tty1 | terminal|
|2024-03-24 08:19 | login date and time|

Command `w` displays information about currently logged in users and what each user is doing. The header shows the same information like [uptime](#how-long-server-is-up) command

```bash
$ w
 17:20:49 up  9:05,  1 user,  load average: 0.55, 0.58, 0.67
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
user     tty1     -                08:16    9:05m  0.16s  0.16s /usr/bin/process
```

Command `users` prints usernames of all users currently logged on the system.

```bash
$ users
user user user
```

Command `last` prints a listing of last logged in users

```bash
$ last
user     pts/4        :1               Sun Mar 24 17:20 - 17:26  (00:05)
user     pts/3        :1               Sun Mar 24 17:20 - 17:20  (00:00)
user     pts/3        :1               Sun Mar 24 10:05 - 11:05  (01:00)
user     pts/1        :1               Sun Mar 24 08:19   still logged in
user     pts/0        :1               Sun Mar 24 08:16   still logged in
user     tty1                          Sun Mar 24 08:16   still logged in
reboot   system boot  6.6.9-amd64      Sun Mar 24 08:15   still running
...
```

Command `lastlog` prints the most recent login of all users or of a given user

```bash
$ lastlog
Username         Port     From                                       Latest
root                                                                **Never logged in**
daemon                                                              **Never logged in**
bin                                                                 **Never logged in**
sys                                                                 **Never logged in**
...
sddm                                                                **Never logged in**
polkitd                                                             **Never logged in**
rtkit                                                               **Never logged in**
user             tty2                                               Mon Mar 11 19:56:37 +0300 2024
```

## File Management

### Which files are located in some directory

To answer this question, we have `ls` command, which **l**i**s**ts directory contents of files and directories:

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

### How create a file

We can use `touch` command to create new empty file(s). Touch is also used to change timestamps on existing files and directories.

```bash
$ touch file1.txt
$ ls
file1.txt
```

Also we can create empty file with `>` - redirect standart output to file
> [!WARNING]
> always overwrites/destroys the previous content

```bash
$ > file2.txt
$ ls
file1.txt file2.txt
```

Finally we can create file with editors like vi, nano, emacs, gedit etc.

### How to remove a file

Just use `rm` (remove) command:

```bash
$ rm file1.txt
# file file1.txt has been removed
```

### How to read a file

The `cat` command is used to concatenate files and print on the standard output:

```bash
$ cat file2.txt
# some content
```

### Determine file type

The `file` command is used to know the file type.

```bash
$ file file2.txt
file2.txt: ASCII text
```

### Copy file

The `cp` (copy) command copy file from source to destiantion:

```bash
$ cp file2.txt file1.txt
$ ls
file1.txt file2.txt
# file2.txt copied to file1.txt
```

### How to rename a file

We can rename a file with `mv` (move) command:

```bash
$ mv file2.txt file3.txt
$ ls
file1.txt file3.txt
# file2.txt moved (renamed) to file3.txt
```
