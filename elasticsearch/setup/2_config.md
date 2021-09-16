### Setting JVM
```
vi /appl/elasticsearch/config/jvm.options
# set memory max 50% dari memori fisik dan tidak boleh lebih dari 32GB
-Xms32g
-Xmx32g
```
### Create Certificate Simpel
```
$ cd /appl/elasticsearch/bin
$ elasticsearch-certutil ca
$ elasticsearch-certutil cert --ca elastic-stack-ca.p12
$ mv elastic-certificates.p12 /appl/elasticsearch/config
$ chmod /appl/elasticsearch/config/elastic-certificates.p12
```
### Create Certificate
```
$ cat <<EOF | /home/vagrant/instance.yml
instances:
  - name: 'server1'
    dns: [ 'server1.example.com' ]
    ip: [ '192.168.0.11' ]
  - name: "server2"
    dns: [ 'server2.example.com' ]
    ip: [ '192.168.0.12' ]
  - name: 'server3'
    dns: [ 'server3.example.com' ]
    ip: [ '192.168.0.13' ]
  - name: 'centos-8'
    dns: [ 'centos-8.example.com' ]
    ip: [ '192.168.0.14' ]
EOF

$ elasticsearch-certutil cert --keep-ca-key ca --pem --in instance.yml --out certs/certs.zip
```
### Edit Environment File
```
$ sudo vi /etc/sysconfig/elasticsearch
MAX_OPEN_FILES=unlimited
MAX_LOCKED_MEMORY=unlimited
MAX_MAP_COUNT=262144
```
### elasticsearch.yml