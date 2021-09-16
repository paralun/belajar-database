### Download Elasticsearch
```
$ curl -L -o elasticsearch-7.14.1-linux-x86_64.tar.gz https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.14.1-linux-x86_64.tar.gz
$ mv elasticsearch-7.14.1-linux-x86_64.tar.gz /appl
$ tar xzvf /appl/elasticsearch-7.14.1-linux-x86_64.tar.gz
$ mv /appl/elasticsearch-7.14.1 /appl/elasticsearch
$ mkdir -p /data/elasticsearch/
```
### Create Service
```
$ sudo cat <<EOF | sudo tee /usr/lib/systemd/system/elasticsearch.service
[Unit]
Description=Elasticsearch
Documentation=https://www.elastic.co
Wants=network-online.target
After=network-online.target

[Service]
Type=notify
RuntimeDirectory=elasticsearch
PrivateTmp=true
Environment=ES_HOME=/appl/elasticsearch
Environment=ES_PATH_CONF=/appl/elasticsearch/config
Environment=PID_DIR=/appl/elasticsearch
Environment=ES_SD_NOTIFY=true
EnvironmentFile=-/appl/config/elasticsearch

WorkingDirectory=/appl/elasticsearch

User=webmethod
Group=webmethod

ExecStart=/appl/elasticsearch/bin/systemd-entrypoint -p ${PID_DIR}/bin/elasticsearch.pid --quiet

StandardOutput=journal
StandardError=inherit

LimitNOFILE=infinity
LimitNPROC=4096
LimitAS=infinity
LimitFSIZE=infinity
TimeoutStopSec=0
KillSignal=SIGTERM
KillMode=process
SendSIGKILL=no
SuccessExitStatus=143
TimeoutStartSec=75

[Install]
WantedBy=multi-user.target
EOF

$ sudo systemctl daemon-reload
$ sudo systemctl enable elasticsearch
$ sudo systemctl start elasticsearch
$ sudo systemctl stop elasticsearch
```