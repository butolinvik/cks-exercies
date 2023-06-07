kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.1.0/aio/deploy/recommended.yaml
kubectl -n kubernetes-dashboard get pod,svc

kubectl -n kubernetes-dashboard get sa
