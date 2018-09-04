# Ansible zookeeper

Reuse most of the code in https://github.com/AnsibleShipyard/ansible-zookeeper


## Running locally:
You will need to have vagrant installed and vagrant-hostmanager plugin


```
vagrant pluin install vagrant-hostmanager
```

Provision a 3 nodes zookeeper cluster:

```
vagrant up
```

```
➜  ~ vagrant ssh zookeeper01 -c  "sudo echo srvr |nc localhost 2181"

Zookeeper version: 3.5.3-beta-8ce24f9e675cbefffb8f21a47e06b42864475a60, built on 04/03/2017 16:19 GMT
Latency min/avg/max: 0/0/0
Received: 7
Sent: 6
Connections: 1
Outstanding: 0
Zxid: 0x0
Mode: follower
Node count: 5

➜  ~ vagrant ssh zookeeper02 -c  "sudo echo srvr |nc localhost 2181"

Zookeeper version: 3.5.3-beta-8ce24f9e675cbefffb8f21a47e06b42864475a60, built on 04/03/2017 16:19 GMT
Latency min/avg/max: 0/0/0
Received: 8
Sent: 7
Connections: 1
Outstanding: 0
Zxid: 0x100000000
Mode: leader
Node count: 5


➜  ~ vagrant ssh zookeeper03 -c  "sudo echo srvr |nc localhost 2181"

Zookeeper version: 3.5.3-beta-8ce24f9e675cbefffb8f21a47e06b42864475a60, built on 04/03/2017 16:19 GMT
Latency min/avg/max: 0/0/0
Received: 2
Sent: 1
Connections: 1
Outstanding: 0
Zxid: 0x100000000
Mode: follower
Node count: 5

```






