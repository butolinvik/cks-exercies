# Use Network security policies to restrict cluster level access
# Use CIS benchmark to review the security configuration of Kubernetes components (etcd, kubelet, kubedns, kubeapi)
# Properly set up Ingress objects with security control
# Protect node metadata and endpoints
# Minimize use of, and access to, GUI elements
# Verify platform binaries before deploying
#=============Certificates===========
- Где лежат сертификаты?
apiserver.crt /etc/kubernetes/pki/apiserveer.crt  ....apiserver.key
Сертифкаты kubelet
/etc/kubernetes/pki/apiserver-kubelet-client.crt

- Сертификаты etcd
