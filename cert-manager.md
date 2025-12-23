# Cert-manager official installation

Intended to work with cluster issuer and gateways

helm install \
  cert-manager oci://quay.io/jetstack/charts/cert-manager \
  --version v1.19.2 \
  --namespace cert-manager \
  --create-namespace \
  --set crds.enabled=true


kubectl apply -f "https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.0.0/standard-install.yaml"

### new feature to renew certificates for gateways
helm upgrade --install cert-manager oci://quay.io/jetstack/charts/cert-manager --namespace cert-manager \
  --set "extraArgs={--enable-gateway-api}"

kubectl rollout restart deployment cert-manager -n cert-manager
