---
description: mencari osd yang menyimpan volume by volume id
---

# \[CEPH] Find OSD storing the volume

ditujukan untuk troubleshot vm yang sedang mengalami perlambatan, sehingga di tuntut untuk mencari osd number agar dapat di analisa lebih lanjut.

Informasi yang harus di dapat terlebih dahulu :

* instance id
* volume id&#x20;
* pool&#x20;

Guide:

#### on Openstack CLI

<pre><code><strong>1. find volume id
</strong>openstack server show &#x3C;instance-id>
<strong>2. find pool 
</strong>openstack server show &#x3C;volume-id> | grep type
</code></pre>

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

#### on Ceph Mon&#x20;

```
3. on ceph mon , check pool name
ceph osd pool ls
4. check volume on pool
rbd -p <pool> ls | grep <id-volume>
5. check pg and osd yang menyimpan volume tersebut
ceph osd map <pool> volume-<id-volume>
```

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

anda akan mendapatkan info :&#x20;

pg 20.6f42b99c (20.399c) -> up (\[378,794,546], p378) acting (\[378,794,546], p378)

pg id : 20.6f42b99c (20.399c)

osd : 378,794,dan 546 , untuk primary ada di 378
