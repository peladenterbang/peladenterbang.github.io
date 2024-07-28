# 💽 Linux File Structure

### File system Explain

Software is composed of file and directory structures. Each file and directory serves a specific purpose. Together, they create the overall system's functionality, allowing it to carry out its tasks. Understanding these structures and how they interact is an essential part of creating, maintaining and troubleshooting software.

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption><p>directory under root</p></figcaption></figure>

Linux file systems are organized according to a standard structure. Directories and files are arranged in a hierarchical structure beginning with the **root** directory at the top. Subdirectories are nested within other directories, with each directory potentially containing files and further subdirectories. This structure allows for easy navigation through the filesystem.&#x20;



<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption><p>Linux file system Hierarchy</p></figcaption></figure>

The main directories are root, home, bin, boot, dev, etc, usr, sbin, lib, tmp and lost+found. Each directory has a distinct purpose like root is the top-level directory and home contains user-specific information. The other directories play a part in managing the system, storing shared files, setting up devices and managing memory. Knowing and utilizing these directories properly is essential for any Linux user.

### 1. / (root)

The root directory (often referred to simply as "/") is the topmost directory in a Linux (or Unix-like) filesystem. It contains all the other directories and files in the filesystem, and is the starting point when navigating the filesystem. It is represented in Linux as a forward slash (/) and should never be renamed, moved, or deleted.

### 2. /boot

the `/boot` directory contain files required to starting your system. don't add or change anything files inside this directory, if you don\`t want to feel the pain when troubleshot because your system doesn't want to boot up. But, if you are an expert, its gonna be okay and you will say "i can do this with root privilages". :D

### 3. /etc

The /etc directory is the vital part of operating system that storing configuration files. These files can be edited to costumize to the system by user preferences. A "configuration file" is a local file used to control the operation of a program. it must be static and cannot be an executable binary. It is recommended that files be stored in subdirectories of `/etc` rather than directly in `/etc`.

### 4. /bin

the `/bin` directory, It contains executable programs and shell scripts. As such, it is a common place for system adminstrators and users to store and launch programs. The directory is also responsible for storing of essential commands for the system, as well as the shells like `bash` and `zsh`. All the binaries in this directory are essential for the proper functioning of a Linux system, making it an important directory.

### 5. /dev

The directory /dev in a Linux file system contains special device files. These files are used to communicate with the hardware devices connected to the computer system and allow user-level programs to access different hardware components. The directory has both character and block device files, which are managed by the kernel and represent hardware like terminals, printers, monitors, and serial ports.

### 6. /var

the `/var` directory contain variable data. This directory store the supporting files for running services like the databases, library, and logs. System administrators often store user information and programs in subdirectories of /var, such as /var/mail, /var/www and /var/ftp. Any services such as web and ftp servers that require constantly updating information will often store their files in /var.

### 7. /home

The /home directory is the default directory for storing personal files for each user in Linux. It typically includes subdirectories for music, documents, pictures, and other personal data. This directory is also used for storing settings for application software. It is a critical aspect of the security environment as it allows users to manage their own private data without affecting other users. The /home directory is typically owned by its respective user, providing users exclusive access to their data.

### Accessing directory

The easiest way to accessing directory is to use the `cd` command. This will change the current directory to the one specified. You can also use the `ls` command to list the contents of the directory, or `pwd` to view the current directory.

```
## for access directory examples :
$ cd /etc
$ cd /var/log
$ cd /home/ubuntu/Document

## how to access same level directory 
catur@ubuntu:~$ cd /var/log/
catur@ubuntu:/var/log$ cd ../lib

## how to back to parent directory
catur@ubuntu:~$ cd /var/lib
catur@ubuntu:/var/lib$ cd ..
catur@ubuntu:/var$
 
## how to back to user home directory
catur@ubuntu:/var/lib$ cd
catur@ubuntu:~$  

## how to list directory , with ls  
catur@ubuntu:/var$ ls
backups  cache  crash  lib  local  lock  log  mail  opt  run  snap  spool  tmp

## how to see current directory 
catur@ubuntu:/etc/dhcp/dhclient-enter-hooks.d$ pwd
/etc/dhcp/dhclient-enter-hooks.d

```

reference :&#x20;

* [https://refspecs.linuxfoundation.org/FHS\_3.0/fhs/index.html](https://refspecs.linuxfoundation.org/FHS\_3.0/fhs/index.html)
* [https://www.linuxfoundation.org/blog/blog/classic-sysadmin-the-linux-filesystem-explained](https://www.linuxfoundation.org/blog/blog/classic-sysadmin-the-linux-filesystem-explained)
