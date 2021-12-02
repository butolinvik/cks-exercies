Restrict access to Kubernetes API
# Use Role Based Access Controls to minimize exposure
создать в разных пространствах имен роли и проверить возможность выолнения
Role and RoleBinding
ClusterRole ClusterRoleBinding
Accounts and Users
    ServiceAccount

    normal users
Certificat request
Последовательность действия
create key- > create csr -> API ->download crt from API - > use crt+key
openssl genrsa -out vik.key 2048
openssl req -new -key vik.key -out vik.csr (fqdn набирам валидное имяп ользователя. Например vik)
Ищем в документации как делать запросы сертификата
vim csr.yaml
В поле request кладем запрос csr в base64 формате
Чтобы получить файл в base 64,делаем cat vik.csr | base64 -w 0
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: vik
spec:
  request: csr request text
  signerName: kubernetes.io/kube-apiserver-client
  expirationSeconds: 86400  # one day
  usages:
  - client auth

kubectl create -f csr.yaml 
kubectl get csr
kubectl certificate approve vik
kubect get csr
Вытаскиваем сертификат
kubectl get csr/vik -oyaml
Копируем поле certificate переводим в base64 и записываем в файл vik.crt
cat certificatetext | base64 -d >vik.crt
ТЕперь надо добавить в конфигурацию
kubernetes config view
kubectl config view
Меняем конфиг для вновь созданного пользователя
kubectl config set-credentials vik --client-key=vik.key --client-certificate=vik.crt
kubectl config view Смотрим изменения
kubectl config set-credentials vik --client-key=vik.key --client-certificate=vik.crt --embed-certs
cat /.kube/config Видим, что в файл записался сертификат
Добавить  контескст
kubectl config set-context vik --user=vik --cluster=kubernetes
k config view
k config get-context
Поменять контекс
kubectl config use-context vik
kubectl config get-contexts

-- Service account --


Создать servicaccount. Исследовать получившийся объект.  Обратите внимание, что сразу появился объект secret, ассоциируемый
Exercise caution in using service accounts e.g. disable defaults, minimize permissions on newly created ones
Update Kubernetes frequently