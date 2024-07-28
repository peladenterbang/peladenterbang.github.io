# 👥 User Management

In this part you will learn about user management on linux operating system. System Administrator need to have knowledge to manage users, this includes creating, deleting, modifying and monitoring user accounts, as well as setting user passwords, allocating disk space, setting permissions, and assigning user roles follow best practices that can be seen in the official documentation for each existing distro. Users must be authenticated by the system in order to access resources and perform tasks, and system administrators can manage these authentication processes.

most powerful user is root with group root, you can editing all file inside linux system. BE CAREFUL !! its very dangerous, you can suicide your system by self with root user. if you use root user, make sure you  not exec with unplanned command.

<img src="../../.gitbook/assets/file.excalidraw (3).svg" alt="" class="gitbook-drawing">

### 1. Creating User

to create new user you need have root or sudo privileges. what is sudo privileges? sudo "super user do" is a privilages given to the user to run of another users(most often root user).

{% hint style="info" %}
[https://www.linux.com/training-tutorials/linux-101-introduction-sudo/](https://www.linux.com/training-tutorials/linux-101-introduction-sudo/)
{% endhint %}

best practice, you can create group before create user.

<img src="../../.gitbook/assets/file.excalidraw (5).svg" alt="" class="gitbook-drawing">

```
## creating group
groupadd ops

## creating user
useradd andy

## add password for andy
passwd andy

## assign user andy to ops group
usermod -g ops andy

## add home directory for andy
mkdir /home/andy
usermod andy -d /home/andy
```

### 2. Deleting user

you can deleting user with any option,

```
catur@ubuntu:~/workdir$ userdel --help
Usage: userdel [options] LOGIN

Options:
  -f, --force                   force removal of files,
                                even if not owned by user
  -h, --help                    display this help message and exit
  -r, --remove                  remove home directory and mail spool
  -R, --root CHROOT_DIR         directory to chroot into
      --extrausers              Use the extra users database
  -Z, --selinux-user            remove any SELinux user mapping for the user
  
## user delete all of home users files 
catur@ubuntu:~/workdir$ userdel -fr andy

## user delete any selinux mapping
catur@ubuntu:~/workdir$ userdel -Z andy

## user delete any selinux mapping and all users file 
catur@ubuntu:~/workdir$ userdel -fzZ andy
```

### 3. User Expiration

on linux you can configure of user expiration. (chage command)

```
## to check expiration list
catur@ubuntu:~/workdir$ chage -l catur
Last password change                                    : Mar 16, 2022
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7

## how to set Maximum number of days between password change
sudo chage -M 90 andy
sudo chage -l andy

## how to didable expiration 
sudo chage  -M 0 andy

## how to set expiration day by date (format : YYYY-MM-DD)
catur@ubuntu:~/workdir$ sudo chage -E 2023-03-31 andy
catur@ubuntu:~/workdir$ sudo chage -l andy

## how to disable expiration day date 
catur@ubuntu:~/workdir$ sudo chage -E -1 andy
catur@ubuntu:~/workdir$ sudo chage -l andy
```

### 4. Granting sudo access to user account

basically you can grant sudo access to user account just with assign users to sudo group.

```
## add andy user to sudo group
catur@ubuntu:~/workdir$ sudo usermod -aG sudo andy

## you can use sudo privilage but you must sign your password, sometimes it's very anoying 
## how to access sudo privilage without password
root@ca-bastion06:~# USERNAME=<your username>
root@ca-bastion06:~# echo $USERNAME
root@ca-bastion06:~# echo "$USERNAME  ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/$USERNAME
root@ca-bastion06:~# cat /etc/sudoers.d/$USERNAME

## check command use sudo privilages with your account 
## correct if your account can use sudo privilage without password 
```
