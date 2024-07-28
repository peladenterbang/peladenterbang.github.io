# Introduce to console

You can call console or terminal, is an interface computer which build to instruct computer with simple line text (actually not simple :D ).&#x20;

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

**Why use console? why not use desktop?, console is very difficult !!**&#x20;

YES!!, we will use console because if you use desktop how we can automate it?. how can you provisioning a lot of users, file or virtual machine in the same time? don't repeat your self.

for example you can create file 1 to 10 in one command line :&#x20;

```
$ touch file{1...10}.txt
$ ls 
file10.txt  file1.txt  file2.txt  file3.txt  file4.txt  file5.txt  file6.txt  file7.txt  file8.txt  file9.txt
```

or you can remove all file has been created in on command line again. Use \* , to delete all files that start with the word "file", and don't care about the ending or file format.

```
$ rm file*
$ ls

```

now ,if you use desktop. how you can handle it? create file one by one and renamed it one by one ?. Same way if you provisioning a lot many many virtual machine.&#x20;

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

You can use command line to create automated virtual machine with supporting software like terraform or ansible. So that the remaining time allocated can be for coffee break :D .
