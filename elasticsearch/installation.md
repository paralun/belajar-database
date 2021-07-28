## Redhat / Centos
### Disable SWAP
```
$ sudo swapoff -a
$ sed -i '/swap/d' /etc/fstab
```
### Installing from the repository
```
$ sudo rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch

$ cat <<EOF | sudo tee /etc/yum.repos.d/elasticsearch.repo
[elasticsearch]
name=Elasticsearch repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=0
autorefresh=1
type=rpm-md
EOF

$ sudo yum install --enablerepo=elasticsearch elasticsearch
$ sudo systemctl daemon-reload
$ sudo systemctl enable elasticsearch.service
$ sudo systemctl start elasticsearch.service
$ sudo systemctl stop elasticsearch.service
```