# \[CEPH] forgote to take out osd but mon already destroyed

you want to destroy the cluster with ceph-deploy. with command&#x20;

```
ceph-deploy purge <hostname>
```

BUT, you forget to takeout osd. to clear format disk you just exec

```
wipefs --force --all /dev/<disk>\
and restart the node disk will be wipe 
```
