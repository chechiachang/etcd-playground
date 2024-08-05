# WIP project

在 release tag 出來前內容會有增減，請注意。

Content may change before release tag. Use with caution.

# etcd-playground

This is a playground for etcd. It is a simple setup with a single node etcd cluster. The setup is done using docker-compose.

# Motivation

2024 K8s Summit 工作坊教材 Workshop lecture on [2024 Kubernetes Summit](https://k8s.ithome.com.tw/2024/) 
- 需要搭配投影片

### Prerequisites

- local
  - etcdctl
- remote
  - docker
  - docker-compose

Check etcd release at https://github.com/etcd-io/etcd/releases

```bash
etcdctl version

etcdctl version: 3.5.15
API version: 3.5
```

docker and docker-compose

```
docker -v

Docker version 27.0.3, build 7d4bcd8

docker-compose -v

Docker Compose version v2.29.1
```

