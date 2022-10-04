# Deployment of OCP and NKE

## OCP

1. Connect to root@10.42.2.110 using SSH
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
2. Go to Kubernetes > Create Kubernetes Cluster > Production Cluster
3. Use 10.42.2.4 for Control Plane VIP
4. Download the kubeconfig file from Prism Central
5. 