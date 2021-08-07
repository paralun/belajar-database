## Setup minimal
```
$ vim elasticsearch.yml
    xpack.security.enabled: true
    discovery.type: single-node / multiple-node (default)
$ elasticsearch-setup-passwords auto
$ elasticsearch-setup-passwords interactive
```