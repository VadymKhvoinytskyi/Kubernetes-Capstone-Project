# Configure cluster

## enable metrics server
https://docs.siderolabs.com/kubernetes-guides/monitoring-and-observability/deploy-metrics-server

## install cni to enable pods networking
https://docs.siderolabs.com/kubernetes-guides/cni/deploying-cilium

use helm installation

### delete flannel
kubectl -n kube-system delete ds kube-flannel --ignore-not-found
kubectl -n kube-system delete cm kube-flannel-cfg --ignore-not-found
kubectl -n kube-system delete sa flannel --ignore-not-found
kubectl -n kube-system delete clusterrole flannel --ignore-not-found
kubectl -n kube-system delete clusterrolebinding flannel --ignore-not-found

## install gateway api(traefik) to enable ingress
https://docs.siderolabs.com/kubernetes-guides/advanced-guides/deploy-traefik

## install hetzner ccm
### also creates hcloud secret necessary for csi
kubectl -n kube-system create secret generic hcloud --from-literal=token=


