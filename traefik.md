# Installing Traefik Gateway
kubectl create namespace traefik

helm repo add traefik https://traefik.github.io/charts
helm repo update

helm upgrade --install traefik traefik/traefik \
  --namespace traefik \
  --set providers.kubernetesGateway.enabled=true \
  --set providers.kubernetesIngress.enabled=true

## To ensure traefik can provision loadbalancer in hetzner
kubectl -n traefik patch svc traefik -p '{
  "metadata":{
    "annotations":{
      "load-balancer.hetzner.cloud/location":"nbg1"
    }
  },
  "spec":{
    "type":"LoadBalancer"
  }
}'

## To ensure traefik can forward traefik to all namespaces. Seems to be particularly important for certificate obtaining
kubectl patch gateway -n traefik traefik-gateway --type='json' -p='[
  {"op":"add","path":"/spec/listeners/0/allowedRoutes","value":{"namespaces":{"from":"All"}}}
]'


### for some reason hetzner ccm struggles to add servers to load balancer by name and id is not added on server creation(potentially missing kubelet flag during installation)
kubectl patch node talos-worker-1 --type=merge -p '{"spec":{"providerID":"hcloud://115825191"}}'
kubectl patch node talos-worker-2 --type=merge -p '{"spec":{"providerID":"hcloud://115967759"}}'

## Gateway to obtain SSL certificates
k apply -f << EOF apiVersion: gateway.networking.k8s.io/v1
kind: Gateway
metadata:
  name: traefik
  namespace: traefik
spec:
  gatewayClassName: traefik
  listeners:
  - name: http
    protocol: HTTP
    port: 80
    allowedRoutes:
        namespaces:
          from: All
EOF


## Create cluster issuer to obtain certificates for all clusters
k apply -f system/cluster-issuer.yaml

## Enable main gateway and dependencies
k apply -f system/gateway.yaml
k apply -f system/gateway-class.yaml
k apply -f system/hcloud-lb.yaml
