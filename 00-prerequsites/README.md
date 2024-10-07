# Prerequisites for workshop

- ssh
- git
- docker
- etcdctl
- demo

### ssh to remote VM

```
ssh -V

ssh-add -i ~/.ssh/chechia-workshop.pem
ssh username@ip
<password>
```

### git

```
git clone git@github.com:chechiachang/etcd-playground.git
cd etcd-playground
```

### docker

```
docker-compose up -d
```

```
docker ps -a
docker logs -f etcd-1
docker exec -it etcd-1
```

### etcdctl

```
export ETCDCTL_API=3

etcdctl member list -h

etcdctl member list

ID, Status, Name, Peer Addrs, Client Addrs, Is Learner
b8c6addf901e4e46, started, etcd-1, http://etcd-1:2380, http://etcd-1:2379, false

etcdctl endpoint health

127.0.0.1:2379 is healthy: successfully committed proposal: took = 608.041µs

etcdctl endpoint status

endpoint, ID, version, db size, is leader, is learner, raft term, raft index, raft applied index, errors.
127.0.0.1:2379, b8c6addf901e4e46, 3.5.15, 22 MB, true, false, 3, 9132, 9132,
```

### demo

https://etcd.io/docs/v3.5/demo/

```
etcdctl put foo k=v
etcdctl get foo

etcdctl role list
etcdctl user list

etcdctl user add root
etcdctl user grant-role root root

export ETCDCTL_USER=root:<password>

etcdctl role add role1
etcdctl role grant-permission role1 readwrite foo
etcdctl user add user1
etcdctl user grant-role user1 role1
etcdctl auth enable

export ETCDCTL_USER=user1:<password>

etcdctl get foo
etcdctl --user=user1 get foo
etcdctl --user=user1:<password> get foo
```

### alias

```
alias e="etcdctl"
e -h

e put foo1 k=v
e put foo2 k=v
e put foo3 k=v
e get foo --prefix

e del foo1
e get foo --prefix
e del foo --prefix
e get foo --prefix
```

### etcdctl continue

https://github.com/etcd-io/etcd/blob/main/etcdctl/README.md

```
e put key1 "1"

e txn -i

# compares:
value("key1") = "1"

# success requests (get, put, delete):
put key2 "success!"

# failure requests (get, put, delete):
put key2 "failed!"

e get key1
e get key2
```

### docker local volume bind

```
ls etcd1/member

ls etcd1/member/snap
db

ls etcd1/member/wal
0000000000000000-0000000000000000.wal

docker-compose down
docker-compose up

docker-compose down
rm -rf etcd1/member
docker-compose up
```

# Issues

- insecure transport

```
{"level":"info","msg":"serving client traffic insecurely; this is strongly discouraged!","traffic":"grpc+http","address":"[::]:2379"}
```
