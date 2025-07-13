# 🏠 Homelab

This repo contains all of the configuration and documentation of my homelab.
The purpose of my homelab is to learn about IaC, GitOps, Linux, Docker, Kubernetes, Proxmox, etc... and to have fun. The purpose of this repository is simply to share how I manage my home lab.

The homelab setup is constantly evolving and being improved. 
Your comments and suggestions are welcome!

## 📋 Quick Overview

| **Component** | **Technology** | **Purpose** |
|---------------|----------------|-------------|

## ️ Architecture

### 🗺️ Network Architecture

```mermaid
---
config:
  theme: neo-dark
---
architecture-beta
  group kubernetescluster(cloud)[VLAN 20 _ Kubernetes Cluster]
  group server(cloud)[VLAN 10]
  service internet(cloud)[Internet] 
  service modem(internet)[Modem]
  service udm(internet)[Virtualized pfSense Router] 
  service switch(internet)[Netgear Switch] 
  service node1(server)[Node_1] in kubernetescluster
  service node2(server)[Node_2] in kubernetescluster
  service node3(server)[Node_3] in kubernetescluster
  service rpi5(server)[Proxmox Server] in server
  junction junctionCenter
  internet:R -- L:modem
  modem:R -- L:udm
  udm:R -- L:switch
  switch:R -- L:junctionCenter
  junctionCenter:B -- L:node1
  junctionCenter:B -- L:node2
  junctionCenter:B -- L:node3
  junctionCenter:B -- T:rpi5
```

### 🗺️ System Architecture

```
```

### 📁 Repository Structure
```

```
