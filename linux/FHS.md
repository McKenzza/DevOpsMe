# Linux File Hierarchy Structure

The Linux File Hierarchy Structure or the Filesystem Hierarchy Standard (FHS) defines the directory structure and directory contents in Unix-like operating systems. It is maintained by the [Linux Foundation](https://wiki.linuxfoundation.org/lsb/fhs).

In the FHS, all files and directories appear under the root directory /, even if they are stored on different physical or virtual devices.
Some of these directories only exist on a particular system if certain subsystems, such as the X Window System, are installed.
Most of these directories exist in all UNIX operating systems and are generally used in much the same way; however, the descriptions here are those used specifically for the FHS and are not considered authoritative for platforms other than Linux.

## Root Directory (/)

Primary hierarchy root and root directory of the entire file system hierarchy.

- Every single file and directory start from the root directory.
- The only root user has the right to write under this directory.
- /root is the root user’s home directory, which is not the same as /

## Organization of Linux File System

The subdirectories include:

|Directory Name|Description|
|-------|--------------------------------------|
| /bin  | essential command-line utilities|
| /boot | static files needed for booting the system|
| /dev  | device files, include terminal devices, usb, or any device attached to the system|
| /etc  | configuration files for the system and various applications|
| /home | Users’ home directories, containing saved files, personal settings, etc.|
| /lib  | libraries essential for binaries in /bin/ and /sbin/|
| /media| mount points for removable media such as CD-ROMs|
| /mnt  | temporarily mounted filesystems|
| /opt  | add-on applications from individual vendors|
| /proc | virtual filesystem providing process and kernel information as files|
| /root | home directory for the root user|
| /sbin | the system executables used typically by system administrators, for system maintenance purposes|
| /sys  | virtual file system that provides an interface to the kernel's device drivers|
| /tmp  | temporary files created by system and users, deleted when the system is rebooted|
| /usr  | user utilities and libraries as well as data shared by multiple users|
| /var  | variable data such as log files, mail spools, and database files|

## Everything is a file

In Linux/Unix operating system everything is a file even directories are files, files are files, and devices like mouse, keyboard, printer, etc are also files.

## Types of files in the Linux system

Files on a Linux system can be divided into three main types:

- **Regular Files** – it is also called ordinary files, it may be an image, video, program, or simple text file. These types of files can be in ASCII or Binary format. It is the most commonly used file in the Linux system.
- **Directory Files** – these types of files are a warehouse for other file types. It may be a directory file within a directory (subdirectory).
- **Special Files** – for devices, tunnels etc.


### Regular Files

Regular files are nothing but the everyday files used to store information such as text, or images. These files can be found in directories, which are yet another type of files. In Linux, regular files can exist with or without an extension.

Example

```bash
$ ls -l /home/user | grep ^-
...
-rw-r--r--   1 root root  1000 Jan 1 16:32 file1.txt
-rw-r--r--   1 root root  1000 Jan 1 17:25 file2.jpg
-rw-r--r--   1 root root  1000 Mar 1 18:25 file3.mp4
...
# listing all the files in the /home/user directory using the `ls -l` command
# The results that begin with '-' will correspond to regular files
```

### Directory files

Linux follows a hierarchical structure to organize files. This is achieved using directories. Directories are also Linux files. But rather than storing data, they store the location of other files. To achieve this, the directory uses directory entries.

Each directory entry stores the name and location of a single file. Linux file system starts with a directory called root (/) directory. All files and directory files are created under this directory. All Linux directories have a parent directory, except the root.

Example

```bash
$ ls -l /home/user | grep ^d
...
drwxr-xr-x   4 root root  4096 Jan 19 20:45 go
drwxr-xr-x   2 root root  4096 Jun 12 16:38 dir1
drwxr-xr-x  16 root root  4096 Oct 24 12:34 dir2
...
# listing all the files in the /home/user/ directory using the `ls -l` command
# filtering the result to display the directory files by using the wildcard ^d
# This will display those lines that begin with the letter 'd'
```

### Special files

The Linux special file can further be divided into five categories:

- Block file
- Character device file
- Named pipe file or just a pipe file
- Symbolic link file
- Socket file

#### Block file

These files are hardware files acting as a direct interface to block devices. A block device is any device that performs data input and output operations in units of blocks. A block special file represents a device that transfers data in blocks such as a hard drive. You can create these files by using the fdisk command or by partitioning. Linux places these files in the /dev directory.

Example

```bash
$ ls -l /dev | grep ^b
brw-rw----   1 root    disk      7,     0 Mar 27 20:07 loop0
brw-rw----   1 root    disk      7,     1 Mar 27 20:07 loop1
brw-rw----   1 root    disk      7,     2 Mar 27 20:07 loop2
brw-rw----   1 root    disk      7,     3 Mar 27 20:07 loop3
brw-rw----   1 root    disk      7,     4 Mar 27 20:07 loop4
brw-rw----   1 root    disk      7,     5 Mar 27 20:07 loop5
brw-rw----   1 root    disk      7,     6 Mar 27 20:07 loop6
brw-rw----   1 root    disk      7,     7 Mar 27 20:07 loop7
brw-rw----   1 root    disk    259,     0 Mar 27 20:07 nvme0n1
brw-rw----   1 root    disk    259,     1 Mar 27 20:07 nvme0n1p1
brw-rw----   1 root    disk    259,     2 Mar 27 20:07 nvme0n1p2
brw-rw----   1 root    disk    259,     3 Mar 27 20:07 nvme0n1p3
# listing block files in the dev directory using the `ls -l` command
# filtering the result to display the block files by using the wildcard ^b
# This will display those lines that begin with the letter 'b'
```

#### Character device file

A character device file is a hardware file that reads or writes data one character at a time in a file. These files provide a serial stream of input or output and provide direct access to hardware devices. Terminal and serial ports come under this category.

Example

```bash
$ ls -l /dev | grep ^c
crw-------   1 root    root     10,   122 мар 27 20:07 acpi_thermal_rel
crw-r--r--   1 root    root     10,   235 мар 27 20:07 autofs
crw-------   1 root    root     10,   234 мар 27 20:07 btrfs-control
crw--w----   1 root    tty       5,     1 мар 27 20:07 console
crw-------   1 root    root     10,   125 мар 27 20:07 cpu_dma_latency
crw-------   1 root    root     10,   203 мар 27 20:07 cuse
crw-------   1 root    root    241,     0 мар 27 20:07 drm_dp_aux0
crw-------   1 root    root    241,     1 мар 27 20:07 drm_dp_aux1
crw-------   1 root    root    241,     2 мар 27 20:07 drm_dp_aux2
crw-------   1 root    root    241,     3 мар 27 20:07 drm_dp_aux3
...
# listing all the files in the dev directory using the `ls -l` command
# filtering the result to display the character files by using the wildcard ^c
# This will display those lines that begin with the letter 'c'
```

#### Named pipe file

Named pipe file also referred to as pipe file is sometimes called FIFO - First In, First Out. It works on the principle that the order of bytes going in is the same as coming out. The “name” of a named pipe is a file name within the file system. This file is responsible for sending data from one process to another so that the receiving process reads the data in FIFO fashion.

Example

```bash
$ mkfifo mypipe
$ ls -l mypipe
prw-r--r-- 1 user user     0 Mar 25 10:19 mypipe
# listing all the files in the dev directory using the ls -l command
# filtering the result to display the pipe files by using the wildcard ^p
# This will display those lines that begin with the letter 'p'
```

##### Test pipe

First terminal:

```bash
$ echo "test message" > mypipe
# send data to tunnel
```

Second terminal:

```bash
$ while read line ;do echo "Data: '$line' "; done<mypipe 
Data: 'test message'
# read data from tunnel
```

#### Symbolic link file

A symbol link file is a special file in Linux that points to another file or a folder. Symbol link files are also called Symlink and are similar to shortcuts in Windows. Link files ensure that we have the flexibility to use a file with a different filename as well as from a different location.

A link file behaves like a pointer to another file. Hard link and soft link are the two types of links. A hard link develops a mirror copy of the original file. A hard link cannot be created for a directory or a file on another filesystem. But a soft or symbolic link creates a pointer to the original file. A soft link can be created to a directory or a file on another filesystem.

Example

```bash
$ ls -l /dev | grep ^l
lrwxrwxrwx   1 root    root            11 мар 27 20:07 core -> /proc/kcore
lrwxrwxrwx   1 root    root            13 мар 27 20:07 fd -> /proc/self/fd
lrwxrwxrwx   1 root    root            12 мар 27 20:07 initctl -> /run/initctl
lrwxrwxrwx   1 root    root            28 мар 27 20:07 log -> /run/systemd/journal/dev-log
lrwxrwxrwx   1 root    root             4 мар 27 20:07 rtc -> rtc0
lrwxrwxrwx   1 root    root            15 мар 27 20:07 stderr -> /proc/self/fd/2
lrwxrwxrwx   1 root    root            15 мар 27 20:07 stdin -> /proc/self/fd/0
lrwxrwxrwx   1 root    root            15 мар 27 20:07 stdout -> /proc/self/fd/1
#  listing all the files in the dev directory using the `ls -l` command
# filtering the result to display the link files by using the wildcard ^l
# This will display those lines that begin with the letter 'l'
```

#### Socket file

Applications use sockets to exchange data. A socket is just a communication endpoint that facilitates this exchange.

When an application wants to interact with another it has to connect with the socket of the other application. The application will use a socket to accept connections. Furthermore, every socket will have an IP address along with a port number associated with it. This allows it to accept connections.

Linux is on the constant lookout to smoothen the communication between local applications. For this it uses socket files. Socket files allow exchange of data without the complicated process of networks and sockets. These special files use a file name as their address instead of IP and port number.

Example

```bash
$ ls -l /var/run | grep ^s
srw-rw----  1 root              docker      0 мар 27 20:07 docker.sock
srwxrwxrwx  1 root              root        0 мар 27 20:07 nvidia-xdriver-4c38c00c
# finding all the files in the /var/run directory using the `ls -l` command
# filtering the result to display the socket files by using the wildcard ^s
# This will display those lines that begin with the letter 's'
```
