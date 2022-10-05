# NKE DEMO


## Scale-Out Node Pools
1. Go to Prism Central
2. Got to Kubernetes
3. Click on the cluster
4. Go to Node Pools > Worker > Actions > Resize
5. Select 4 

## Use Karbon extension to Login using PC
1. On the Jumphost :
   ```bash
   kubectl karbon login --server phx-poc002.ntnx.fr -u admin --force
   kubectl karbon list --server phx-poc002.ntnx.fr -u admin
   ```


## NKE Interface YAML
1. Connect to Prism Central using http://phx-poc002.ntnx.fr
2. Go to Service > Kubernetes > Clusters > demo-nke-dev01
3. Namespace > Select a Namespace (ntnx-system)
4. Click on Workloads and 


## CSI : Files/Volumes

Create a Storage Class on the deployed cluster

Storage Class Name : files-storageclass
Nutanix File Server Address : 10.42.2.47
Share Path : /volume01

Go to persistent volume, and create a volume with:
```bash
- Claim name : demo-pv-files-01
- Storage Class : files-storageclass
- Access Mode : Read Write Once
- Volume : 20 GB
```

After a couple of second, the volume should be seen as Bound

## Database provisioning
Show the databases already deployed
```bash
kubectl get dbs
```
Deploy a new database
```bash
kubectl apply -f ~/demo-fdvs/ndb.yaml
kubectl get dbs -w
```

## Kasten
1. Use nke-01 context
2. Install Kasten using helm
   ```bash
   helm repo add kasten https://charts.kasten.io/
   kubectl create namespace kasten-io
   helm install k10 kasten/k10 --namespace=kasten-io
   helm upgrade k10 kasten/k10 --namespace=kasten-io \
    --reuse-values \
    --set externalGateway.create=true \
    --set auth.tokenAuth.enabled=true
    ```
3. Create a Service account with token
   ```bash
   kubectl create serviceaccount my-kasten-sa --namespace kasten-io
   kubectl create clusterrolebinding my-kasten-sa --clusterrole=cluster-admin --serviceaccount=kasten-io:kasten-sa
   ```
4. Get the access token :
   ```bash
   sa_secret=$(kubectl get serviceaccount my-kasten-sa -o jsonpath="{.secrets[0].name}" --namespace kasten-io)
   kubectl get secret $sa_secret --namespace kasten-io -ojsonpath="{.data.token}{'\n'}" | base64 --decode
   ```
5. Access to Kasten using http://10.42.2.XXX/k10/?page=Login#/login
6. Go to Settings > Location Profiles > S3 Compatible
7. Use the following configuration and Secret keys
   1. Access
   ```9gxL7j4U81a-iPaLZpVdePZNzRmC0KR8```
   2. Secret
   ```LxFA2Wy6qNsbJ8PpChJtIer_ZWc4GwWu```
   3. Endpoint
   ```10.42.2.18```
   4. Bucket Name
   ```k10```
8. Go to Policy and create a backup policy
9. Create K10 DR

## Upgrade Kubernetes
1. Go to prism Central to upgrade nke-02
