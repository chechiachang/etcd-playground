### CA and TLS Certificates

```
cd 02-control-panel/certs
chmod +x generate.sh
./generate.sh
```

or complete [https://github.com/kelseyhightower/kubernetes-the-hard-way](https://github.com/kelseyhightower/kubernetes-the-hard-way)

- [04-certificate-authority.md]https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/04-certificate-authority.md#provisioning-a-ca-and-generating-tls-certificates

### Docker up

```
cd 02-control-panel
make up
```

### Docker down

```
cd 02-control-panel
make down
```

### Access Control Panel

```
docker ps

IMAGE                                             COMMAND                  STATUS         PORTS                              NAMES
registry.k8s.io/kube-scheduler:v1.31.0            "kube-scheduler --co…"   Up 2 seconds                                      kube-scheduler
registry.k8s.io/kube-controller-manager:v1.31.0   "kube-controller-man…"   Up 2 seconds                                      kube-controller-manager
bitnami/kubectl:1.31.1-debian-12-r3               "sleep 86400"            Up 2 seconds                                      kubectl
registry.k8s.io/kube-apiserver:v1.31.0            "kube-apiserver --bi…"   Up 2 seconds   0.0.0.0:6443->6443/tcp             kube-apiserver
quay.io/coreos/etcd:v3.5.15                       "/usr/local/bin/etcd…"   Up 2 hours     2380/tcp, 0.0.0.0:2380->2379/tcp   etcd-2
quay.io/coreos/etcd:v3.5.15                       "/usr/local/bin/etcd…"   Up 2 hours     0.0.0.0:2379->2379/tcp, 2380/tcp   etcd-1
quay.io/coreos/etcd:v3.5.15                       "/usr/local/bin/etcd…"   Up 2 hours     2380/tcp, 0.0.0.0:2381->2379/tcp   etcd-3
```

kubectl

```
kubectl --kubeconfig=certs/admin.kubeconfig cluster-info

Kubernetes control plane is running at https://127.0.0.1:6443

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

```
kubectl --kubeconfig=certs/admin.kubeconfig get all

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.0.0.1     <none>        443/TCP   47h
```
