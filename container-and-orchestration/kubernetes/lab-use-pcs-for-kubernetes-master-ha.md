# \[LAB] Use PCS for Kubernetes Master HA

```
10.50.0.54 ca-lb1
10.50.0.72 ca-lb2
10.50.0.75 ca-master1
10.50.0.67 ca-master2
10.50.0.84 ca-worker1
10.50.0.55 ca-worker2
10.50.0.42 ca-worker3

# deploy cluster
apt install pcs pacemaker corosync fence-agents
echo HACluster123 | passwd --stdin hacluster
pcs cluster auth ca-lb1 ca-lb2 -u hacluster --force
pcs cluster setup --start --name ha_cluster ca-lb1 ca-lb2 --force

# Since you are running two node cluster, you don't have a fencing device. So you have to disable the STONITH setting but it is not recommended for production environment.
pcs property set no-quorum-policy=ignore
pcs property set stonith-enabled=false
pcs resource create HACluster systemd:haproxy op monitor interval=10 timeout=10 on-fail=restart
pcs resource create VIP ocf:heartbeat:IPaddr2 ip=10.50.0.100 cidr_netmask=24 op monitor interval=1s
pcs resource group add HAproxyGroup VIP HACluster
pcs constraint order VIP then HACluster

# HAproxy
apt install haproxy
nano /etc/haproxy/haproxy.cfg
frontend kubernetes
    bind *:443
    option tcplog
    mode tcp
    default_backend kubernetes-master-nodes

frontend kubernetes_https
    bind *:6443
    option tcplog
    mode tcp
    default_backend kubernetes-master-nodes

backend kubernetes-master-nodes
    mode tcp
    balance roundrobin
    option tcp-check
    server ca-master1 10.50.0.75:6443 check fall 2 rise 1
    server ca-master2 10.50.0.55:6443 check fall 2 rise 1
```
