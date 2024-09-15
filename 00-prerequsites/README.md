# Prerequisites for workshop

- ssh
- docker
- git
- etcdctl

### ssh to remote VM

### docker

```
docker-compose up -d
```

```
docker ps -a
docker logs -f etcd-1
docker exec -it etcd-1
```

### git

```
git clone git@github.com:chechiachang/etcd-playground.git
cd etcd-playground
```

### etcdctl

```
etcdctl member list -h

etcdctl member list

ID, Status, Name, Peer Addrs, Client Addrs, Is Learner
b8c6addf901e4e46, started, etcd-1, http://etcd-1:2380, http://etcd-1:2379, false

etcdctl endpoint health
```
