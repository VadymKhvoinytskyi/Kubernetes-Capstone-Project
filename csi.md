# CSI
## Sync the Hetzner Cloud helm chart repository to your local computer.
helm repo add hcloud https://charts.hetzner.cloud
helm repo update hcloud

## Install the latest version of the csi-driver chart.
helm install hcloud-csi hcloud/hcloud-csi -n kube-system 
