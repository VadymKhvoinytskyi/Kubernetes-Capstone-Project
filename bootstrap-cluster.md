# Bootstrap kubernetes cluster with talos linux on hetzner


## Installing talos linux

Follow instructions described here with adjustments listed below: https://docs.siderolabs.com/talos/v1.8/platform-specific-installations/cloud-platforms/hetzner#hetzner
Apply patches from talos-patches directory to enable talos features necessary for next steps of installation. 

### be aware:
- do not restart machine before taking snapshot, only shutdown
- use image factory to generate appropriate image: https://factory.talos.dev/?arch=amd64&cmdline-set=true&extensions=-&platform=hcloud&target=cloud&version=1.11.6
- do not change primary ip after server is created

To provision new servers use hetzner web interface of hcloud cli.

## Manage cluster from local machine

- install talosctl
- install kubectl
- consider installing kubens and kubectx to streamline navigating between clusters and namespaces
- merge kubeconfig obtained during installation with ~/.kube/config to add cluster to your kubectl
- copy generated talosconfig to enable yourself to manage talos machines

