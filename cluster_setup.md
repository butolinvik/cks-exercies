# Use Network security policies to restrict cluster level access
-- Поды по дефолту видят друг друга, если находятся на одной и той же ноде
# Network Policy
-- Политики Ingress, Egress
-- Перед тем, как настроить CNI надо понимать, что там были уже настройки по умолчанию.(etc/cni/net.d/**.) Если они подхватятся, работать ничего не будет. Поэтому, удаляем старый конфиг, настраиваем новый и перезагружаемся
-  Развернуть поды. Дать доступ снаружи
   kubectl expose pod backend --port=80
   kubectl expose pod backend1 --port=80
   kubectl expose pod frontend --port=80
-  Запретить обмен трафиком
---
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  - Egress

- Разрешить входящй порт 80
- Разрешить исходящий порт 80
- Объединить

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
