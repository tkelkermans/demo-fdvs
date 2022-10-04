# Deployment of OCP and NKE

## OCP

1. Connect to root@10.42.2.63 using SSH
2. Copy folder ocp-backup2 to ocp
   ```bash
   cp -R ocp-backup2 ocp
   ```
3. Create the manifests files for OCP
   ```bash
   openshift-install create manifests
   ```
4. Start the install of OCP
   ```bash
   openshift-install create cluster
   ```
5. Set the KUBECONFIG environment variable
   ```bash
   export KUBECONFIG=/root/ocp/auth/kubeconfig
   ```

## NKE
1. Login to Prism Central on https://phx-poc002.ntnx.fr:9440/console/#login
2. Go to Kubernetes > Create Kubernetes Cluster > Production Cluster > Name it nke-02
3. Use 10.42.2.4 for Control Plane VIP
4. Show that we can download the Kubeconfig fileDownload the kubeconfig file
5. On the jumphost use the kubectl karbon command to retrieve the kubeconfig file 
```bash
kubectl karbon login --server phx-poc002.ntnx.fr -u admin --cluster nke-02
```
6. Show all pods deployed by default
```bash
kubectl get pods -A
```


