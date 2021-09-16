## Redhat / Centos
### Download Elasticsearch
```
$ curl -L -o elasticsearch-7.14.1-x86_64.rpm https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.14.1-x86_64.rpm
```
### Disable SWAP
```
$ sudo swapoff -a
$ sed -i '/swap/d' /etc/fstab
```
### Edit /etc/sysctl.conf
```
$ sudo cat <<EOF>> /etc/sysctl.conf
vm.max_map_count=262144
EOF

$ sysctl vm.max_map_count
```
### Edit /etc/security/limits.conf
```
$ sudo vi /etc/security/limits.conf
webmethod       soft    nproc           unlimited
webmethod       hard    nproc           unlimited
webmethod       soft    sigpending      192068
webmethod       hard    sigpending      192068
webmethod       soft    msgque ue       819200
webmethod       hard    msgqueue        819200
webmethod       soft    nofile          unlimited
webmethod       hard    nofile          unlimited
webmethod       soft    memlock         unlimited
webmethod       hard    memlock         unlimited
webmethod       soft    stack           10240
webmethod       hard    stack           10240
webmethod       soft    core            unlimited
webmethod       hard    core            unlimited
```
### Install Elastic
```
$ rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
$ rpm -ivh elasticsearch-7.14.1-x86_64.rpm
$ sudo systemctl daemon-reload
$ sudo systemctl enable elasticsearch
```
### Directory Installasi Elastic
```
/usr/lib/systemd/system/elasticsearch.service
ES_HOME=/usr/share/elasticsearch
ES_PATH_CONF=/etc/elasticsearch
PID_DIR=/var/run/elasticsearch
ES_SD_NOTIFY=true
EnvironmentFile=-/etc/sysconfig/elasticsearch
```