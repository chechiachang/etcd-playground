# Node

https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/09-bootstrapping-kubernetes-workers.md

```
make up
```

kubeadm

```
docker exec -it node-0 bash
kubeadm config print join-defaults > kubeadm-join-config.yaml
kubeadm join --config kubeadm-join-config.yaml
```
