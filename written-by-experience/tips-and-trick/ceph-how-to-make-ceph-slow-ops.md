---
description: sometimes we need to make the problem to get a solution from the problem
---

# \[CEPH] How to make ceph slow ops

{% hint style="danger" %}
Don't try this on your production ceph cluster
{% endhint %}

#### Topology

<img src="../../.gitbook/assets/file.drawing (3).svg" alt="" class="gitbook-drawing">

#### **Background**

If a `ceph-osd` daemon is slow to respond to a request, messages will be logged noting ops that are taking too long. Then, ceph cluster encounters a slow/blocked operations it will log it and set cluster health into warning mode. The warning threshold defaults to 30 seconds and is configurable via the `osd op complaint time` setting.&#x20;

don't ignore this issue too long, because slow request can impact to performance your storage client to vm or container, and if too bad this issue can causing kernel hung.

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

the root causes of slow request osd are:

* problem with underlaying hardware (disk, ram , processor, etc)
* network problem(flapping, packet drop, latency, miss configuration, time not sync)
* system load

#### **Simulation**

first, access to on of node in the cluster, for example ca-node01, then check load i/o of the disk with nmon.

{% code lineNumbers="true" %}
```bash
apt install nmon
nmon
# then pres d to look disk load 
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

its look like not busy, let's make it busy :D . write file to  disk on all client side will enough make object busy.

{% code overflow="wrap" lineNumbers="true" %}
```bash
head -c 6G /dev/zero > deleteme_6G && ls && rm deleteme_6G && ls
```
{% endcode %}

&#x20;

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

it's look like any object busy, but not with 100% load, so you can adjust on client or file size to make it 100% load. Check status health ceph (are there any slowops?), if any slow ops check location of object storage with `ceph osd tree` on **ceph-mon** to see location object inside node and `ceph-volume lvm list`  on **node** to see location object inside disk storage.&#x20;

* first treatment, you can restart service osd. if slow ops still continues, take the next step.
* stop write test process and check load disk with `nmon` , if load disk still 100%, take out the osd for bad block test.&#x20;
* if there are bad blocks on the disk, do a replacement on the disk.

if you are at this stage I assume there is no problem with the osd, slow ops, or anything. Then, still keep load test on the client. we increase extra load  on the network. create high bandwith use iperf  do cross between nodes:

{% code lineNumbers="true" %}
```bash
iperf -c <dest-ip> -u -t 300 -b 800M

## -t is time in secound 
## -b is bandwith
```
{% endcode %}

{% hint style="info" %}
if you have 10Gig NIC, do the test with 10G, makesure your test with maximum performance.
{% endhint %}

check load traffic network with `nmon` then press n key to see network load.

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

check ceph  health status. If not any ceph slow ops on there, congratulation !! your ceph cluster is really healthy.&#x20;

**Can we make it slow ops (which is on purpose)?, YES, we can do it.**

* First, run disk and network load test.&#x20;
* Currently ceph cluster is in maximum performance, make it same condition on production with load test.&#x20;
* do ping cross a node. see the time latency, showing under 1 ms latency.

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

* adjust latency to make slow response a cross osds.

{% code lineNumbers="true" %}
```bash
## add rule
tc qdisc add dev ens3 root netem delay 30ms
## list tc
tc -s qdisc
## delete rule tc
tc qdisc del dev ens3 root netem
```
{% endcode %}

* then check ceph health status, whalaaa :D,ceph health status will change to warning because slow ops.

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

#### Mitigation

