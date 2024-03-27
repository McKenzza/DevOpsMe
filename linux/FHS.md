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
- **Directory Files** – These types of files are a warehouse for other file types. It may be a directory file within a directory (subdirectory).
- **Device Files** – In a Windows-like operating system, devices like CD-ROM, and hard drives are represented as drive letters like F: G: H whereas in the Linux system devices are represented as files. As for example, /dev/sda1, /dev/sda2, and so on.

### Regular Files

Regular files are nothing but the everyday files used to store information such as text, or images. These files can be found in directories, which are yet another type of files. In Linux, regular files can exist with or without an extension.

Example

```sh
$ ls -l /etc | grep ^-
...
-rw-r--r--   1 root root  1000 Jan 1 16:32 file1
-rw-r--r--   1 root root  1000 Jan 1 17:25 file2
-rw-r--r--   1 root root  1000 Mar 1 18:25 file3
...
```
