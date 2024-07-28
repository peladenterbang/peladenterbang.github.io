# \[K8S] Can't Joining worker to cluster

Error during joining the worker to the cluster :

```
 [ERROR FileContent--proc-sys-net-bridge-bridge-nf-call-iptables]: /proc/sys/net/bridge/bridge-nf-call-iptables does not exist
 
```

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Routcause : not complete pre-requisites node, just see, [https://kubernetes.io/docs/setup/production-environment/container-runtimes/#install-and-configure-prerequisites](https://kubernetes.io/docs/setup/production-environment/container-runtimes/#install-and-configure-prerequisites)

for my issue, i solved with execute the command

```
sudo modprobe br_netfilter
echo '1' > /proc/sys/net/ipv4/ip_forward
```

