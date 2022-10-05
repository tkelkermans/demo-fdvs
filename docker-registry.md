```bash
kubectl create secret docker-registry regcred --docker-server=https://index.docker.io/v1/ --docker-username=xxx --docker-password=xxx -n sock-shop
kubectl patch serviceaccount default -p '{"imagePullSecrets": [{"name": "regcred"}]}' -n sock-shop
```