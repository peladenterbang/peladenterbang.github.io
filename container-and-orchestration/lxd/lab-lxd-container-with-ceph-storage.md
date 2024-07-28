---
description: integrate lxd with ceph storage
---

# \[LAB] LXD container with ceph storage

```
/etc/hosts
10.0.0.34 ca-lxd1
10.0.0.30 ca-lxd2
10.0.0.41 ca-lxd3

virsh attach-disk ca-lxd1 /data/vms/ca-lxd1-vdb.img vdb --driver qemu --subdriver qcow2 --targetbus virtio --persistent

python3 -m venv ceph
cd ceph
. bin/activate
pip3 install git+https://github.com/ceph/ceph-deploy.git

ceph-deploy --username root new ca-lxd1 ca-lxd2 ca-lxd3
ceph-deploy --username root install ca-lxd1 ca-lxd2 ca-lxd3 --release pacific --mon --mgr --mds --osd
ceph-deploy --username root mon create ca-lxd1 ca-lxd2 ca-lxd3
ceph-deploy --username root gatherkeys ca-lxd1 ca-lxd2 ca-lxd3
ceph-deploy --username root admin ca-lxd1 ca-lxd2 ca-lxd3
ceph-deploy --username root mgr create ca-lxd1 ca-lxd2 ca-lxd3
ceph-deploy --username root mds create ca-lxd1 ca-lxd2 ca-lxd3
ceph-deploy --username root osd create --data /dev/vdb ca-lxd1
ceph-deploy --username root osd create --data /dev/vdc ca-lxd1
ceph-deploy --username root osd create --data /dev/vdd ca-lxd1
ceph-deploy --username root osd create --data /dev/vdb ca-lxd2
ceph-deploy --username root osd create --data /dev/vdc ca-lxd2
ceph-deploy --username root osd create --data /dev/vdd ca-lxd2
ceph-deploy --username root osd create --data /dev/vdb ca-lxd3
ceph-deploy --username root osd create --data /dev/vdc ca-lxd3
ceph-deploy --username root osd create --data /dev/vdd ca-lxd3

ceph osd pool create persist-cephfs_data 8
ceph osd pool create persist-cephfs_metadata 8
ceph fs new persist-cephfs persist-cephfs_metadata persist-cephfs_data
ceph fs set persist-cephfs allow_new_snaps true

ceph -s

snap install lxd
lxd init
clustering yes
remote cluster storage yes

join cluster 
lxd init
clustering yes
join existing cluster yes


test


lxc launch images:ubuntu/18.04 --storage remote u2


lxc remote add lxd-cluster 10.0.0.34 --password <your password>
```
