# Kubernetes Capstone Project - Robot Dreams

## Cluster Architecture

![](Kuber.drawio.svg)


## Roadmap

- evaluate cilium vs flannel
- evaluate gateway vs ingress (vs ingressroute?) (speed difference?)
- automate dns
- worker communication over private network
- s3 for rwx storage
- storage pool like longhorn/cephfs/storageos
- improve security
- improve resource utilization

## Kubernetes System Objects deployed

- cilium cni
- hetzner ccm
- hetzner csi
- metrics server
- traefik ingress and gateway
- cert-manager

## Apps deployed

- cnpg with helm (storage)
- nextcloud with helm (storage, postgres connection)
- excalidraw with manifest (stateless)
