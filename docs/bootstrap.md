---
hide:
  - toc
---

# Bootstrap

[https://github.com/matt328/bootstrap](https://github.com/matt328/bootstrap)

This project, which needs to be renamed and documented, is a 'live' repo that declaratively manages
my kubernetes homelab.

It uses ArgoCD to declaratively manage all the software and tools I have installed in my homelab's
kubernetes cluster. This repository documents the process to install kubernetes using k3s, and from
there goes through the process of 'bootstrapping' the cluster by installing a few prerequisite tools
and then installing ArgoCD and finally configures ArgoCD to manage everything installed so far, including
itself.

Current tools and technologies include:

- Kubernetes using k3s
- Bitnami Sealed Secrets
- MetalLB to expose services to my local network
- Longhorn for storage management and backup
- A private gitea instance that holds mirrors of most of my github projects as well as provides more
  efficient runners for continuous integration
- An initial POC of Grafana's LGTM stack for monitoring and observability.

My current 'homelab' configuration uses several VMs on an Ubuntu host with a Raspberry PI serving an
NFS share for Longhorn backups.
