# NKE DEMO

## Upgrade Kubernetes

## Scale-Out Node Pools
1. Go to Prism Central
2. Got to Kubernetes
3. Click on the cluster
4. Go to Node Pools > Worker > Actions > Resize
5. Select 4 

## Use Karbon extension to Login using PC
1. On the Mac :
   ```bash
   kubectl karbon login --server phx-poc002.ntnx.fr -u admin --force
   kubectl karbon list --server phx-poc002.ntnx.fr -u admin
   ```


## NKE Interface YAML
1. Connect to the Prism Central VM using SSH
   ```bash
   ssh nutanix@phx-poc002.ntnx.fr
   ```
2. From the Prism Central VM, use the karbonctl command to enable advanced Kubernetes management.
   ```bash
    /home/nutanix/karbon/karbonctl login --pc-username admin
    /home/nutanix/karbon/karbonctl karbon-management enable --cluster-name nke-02
    ```

## CSI : Files/Volumes

## Kasten
1. Login to argocd and create the new cluster deployed :
   ```bash
   argocd login
   ```
