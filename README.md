# Homelab Infrastructure

This repository contains the configuration and documentation for my homelab infrastructure.
The primary goal of this homelab is to provide a robust, secure, and scalable environment for learning about IaC, GitOps, Linux, Docker, Kubernetes, Proxmox, and networking concepts. The purpose of this repository is to share the management and configuration of this environment.

The homelab setup is constantly evolving and being improved. 
Your comments and suggestions are welcome!

## Quick Overview

| **Component** | **Technology** | **Purpose** |
|---------------|----------------|-------------|
| **Virtualization** | Proxmox VE | Central hypervisor for all virtual machines (pfSense, Pi-hole, Traefik). |
| **Networking/VPN** | pfSense + Tailscale | Virtualized firewall/router and secure, private overlay network for remote access (Subnet Router). |
| **DNS/Ad-blocking** | Pi-hole | Internal DNS resolution and network-wide ad-blocking. |
| **Reverse Proxy** | Traefik | Central ingress point for all services, handling routing and TLS termination. |
| **Orchestration** | Kubernetes (3-Node) | Application hosting and container orchestration on dedicated hardware. |
| **GitOps** | ArgoCD | Declarative infrastructure management (Planned). |
| **Monitoring** | Prometheus + Grafana | Comprehensive observability stack (Planned). |

## ️ Architecture

### Network Architecture

The network is built around a secure, layered approach:

1.  **Gateway & Firewall:** A virtualized **pfSense** instance acts as the main router and firewall, managing the LAN subnet.
2.  **Remote Access:** **Tailscale** is installed on pfSense and configured as a **Subnet Router**, securely exposing the entire LAN to the Tailnet for remote access without port forwarding.
3.  **DNS Resolution:** A dedicated **Pi-hole VM** handles all internal DNS. It is configured in pfSense's DHCP settings and in the Tailscale Admin Console to resolve all internal FQDNs (e.g., `service.home`).
4.  **Service Ingress:** A dedicated **Traefik VM** acts as the single entry point. All internal FQDNs resolve to this VM's IP via Pi-hole.

### System Architecture

The services are distributed across the Proxmox hypervisor and dedicated hardware:

| Host Platform | Components | Role |
| :--- | :--- | :--- |
| **Proxmox VE** | pfSense VM | Virtualized Router/Firewall/Tailscale Subnet Router. |
| **Proxmox VE** | Pi-hole VM | Dedicated internal DNS server. |
| **Proxmox VE** | Traefik VM | Dedicated Reverse Proxy and Load Balancer (Docker-based). |
| **Dedicated Hardware** | 3-Node Kubernetes Cluster | Hosts all production applications, exposed via `NodePort` services. |

### Repository Structure
