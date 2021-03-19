
# Simple setup

Simple example setting up *glusterfs geo-replication* on *Debian 10*

### host1
```bash
apt-get install gluster -y
apt-get install samba -y
apt-get install rsync -y
gluster volume create vol1 node1.smartdom.ch:/srv/gluster_data/vol1 force
gluster volume start vol1
mount.glusterfs node1.smartdom.ch:/vol1 /root/data
```

### host2
```bash
apt-get install gluster -y
apt-get install samba -y
apt-get install rsync -y
gluster volume create vol1_c node2.smartdom.ch:/srv/gluster_data/vol1_c force
gluster volume start vol1_c
mkdir /root/data
mount.glusterfs node2.smartdom.ch:/vol1_c /root/data
```


### host1
```bash
ssh-keygen
#add ssh key on host2
gluster system:: execute gsec_create
gluster volume geo-replication vol1 node2.smartdom.ch::vol1_c create push-pem
gluster volume geo-replication vol1 node2.smartdom.ch::vol1_c config use_meta_volume false
gluster volume geo-replication vol1 node2.smartdom.ch::vol1_c config access_mount true
gluster volume geo-replication vol1 node2.smartdom.ch::vol1_c start
gluster volume geo-replication vol1 node2.smartdom.ch::vol1_c status
```
