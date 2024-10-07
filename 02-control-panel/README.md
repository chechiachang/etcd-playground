### CA and TLS Certificates

https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/04-certificate-authority.md#provisioning-a-ca-and-generating-tls-certificates

```
cd certs

openssl genrsa -out ca.key 4096
openssl req -x509 -new -sha512 -noenc \
  -key ca.key -days 3653 \
  -config ca.conf \
  -out ca.crt
```

Check

```
ls ca.*
ca.conf ca.crt  ca.key
```

### Generate certificates

```
certs=(
  "admin" "node-0" "node-1"
  "kube-proxy" "kube-scheduler"
  "kube-controller-manager"
  "kube-apiserver"
  "service-accounts"
)

for i in ${certs[*]}; do
  mkdir -p ${i}
  openssl genrsa -out "${i}/${i}.key" 4096

  openssl req -new -key "${i}/${i}.key" -sha256 \
    -config "ca.conf" -section ${i} \
    -out "${i}/${i}.csr"

  openssl x509 -req -days 3653 -in "${i}/${i}.csr" \
    -copy_extensions copyall \
    -sha256 -CA "ca.crt" \
    -CAkey "ca.key" \
    -CAcreateserial \
    -out "${i}/${i}.crt"
done
```

Output

```
Certificate request self-signature ok
subject=CN=admin, O=system:masters
Certificate request self-signature ok
subject=CN=system:node:node-0, O=system:nodes, C=TW, ST=Taiwan, L=Taichung
Certificate request self-signature ok
subject=CN=system:node:node-1, O=system:nodes, C=TW, ST=Taiwan, L=Taichung
Certificate request self-signature ok
subject=CN=system:kube-proxy, O=system:node-proxier, C=TW, ST=Taiwan, L=Taichung
Certificate request self-signature ok
subject=CN=system:kube-scheduler, O=system:system:kube-scheduler, C=TW, ST=Taiwan, L=Taichung
Certificate request self-signature ok
subject=CN=system:kube-controller-manager, O=system:kube-controller-manager, C=TW, ST=Taiwan, L=Taichung
Certificate request self-signature ok
subject=CN=kubernetes, C=TW, ST=Taiwan, L=Taichung
Certificate request self-signature ok
subject=CN=service-accounts
```

Check

```
ls -1 *.crt *.key *.csr

admin.crt
admin.csr
admin.key
ca.crt
ca.key
kube-apiserver.crt
kube-apiserver.csr
kube-apiserver.key
kube-controller-manager.crt
kube-controller-manager.csr
kube-controller-manager.key
kube-proxy.crt
kube-proxy.csr
kube-proxy.key
kube-scheduler.crt
kube-scheduler.csr
kube-scheduler.key
node-0.crt
node-0.csr
node-0.key
node-1.crt
node-1.csr
node-1.key
service-accounts.crt
service-accounts.csr
service-accounts.key
```
