# AI Virtual Machine Setup

## Overview

This project documents my AI-focused virtual machine lab running on a Proxmox environment in node 2.  
It is used for Linux administration, networking, and deploying AI-related services in isolated VMs.

The goal is to simulate real-world infrastructure for AI workloads and self-hosted tools.

---

## Objectives

- Build and manage virtual machines in Proxmox
- Deploy AI tools and services in isolated environments
- Learn networking between VMs and host system
- Practice Linux system administration
- Explore containerized AI workloads
- Set up tailnet for use outside of home network

---

## Architecture

- Linux-based VM (xubuntu)
- Docker-based applications
- Internal networking between services

(Add diagram in /images/architecture.png)

---

## Virtual Machine

### AI Service VM
- OS: xUbuntu Desktop
- Role: AI tools / container runtime
- Services:
  - Docker
  - LmStudio
  - Anythingllm (docker image)
  - API services
    
---

## Installation Summary

1. Installed Proxmox VE on host machine
2. Created base Linux VM templates
3. Deployed AI service VM using template
4. Installed Docker and dependencies
5. Configured networking between VMs
6. Deployed AI services via Docker Compose

---

## Networking

- Static IP assignment for VMs
- Bridge networking via Proxmox (vmbr0)
- Tailscale

---

## Skills Demonstrated

- Virtualization (Proxmox VE)
- Linux system administration
- Networking and IP management
- Docker and containerization
- Infrastructure documentation
- Basic AI service deployment
- PCIE passthrough and other tools
  
---

## Future Improvements

- GPU passthrough for AI acceleration
- Kubernetes cluster expansion
- More isolated service VMs
- Automated VM provisioning scripts
