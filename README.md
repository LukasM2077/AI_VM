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

![image_api](https://github.com/LukasM2077/AI_VM/blob/main/images/Screenshot%202026-06-24%20182925.png?raw=true)

## Architecture

- Linux-based VM (xubuntu)
- Docker applications
- Internal networking between services

---

## Virtual Machine

- OS: xUbuntu Desktop
- Role: AI tools / container runtime
- Services:
  - Docker
  - LmStudio
  - Tailscale
  - Anythingllm (docker image)
  - API services
    
---

## Installation Summary

- Created the VM
  Installed xubuntu (desktop) iso and loaded it into proxmox. Set and assigned ram, cpu cores, and storage.

- installed LmStudio
   1. went to LmStudio's website and downloaded the linux appimage on the vm.
   2. created a folder for LmStudio (lmstudio) in home. Moved appimage to new folder.
   3. give appimage file permissions. cd into the folder and use chmod (chmod u+x LM-Studio-0.4.2.2-64x.AppImage)

      IMAGE

    4. execute and extract appimage (./LM-Studio-0.4.2.2-64x.AppImage --appimage-extract
    5. enter the new folder squashfs-root
    6. set permissions in squashfs using (sudo chown root:root chrome-sandbox) and (sudo chmod 4755 chrome-sandbox)
    7. run the program (./lm-studio)

  Easy startup
  instead of having to navigate to squashfs-root each time to run lmstudio, I created an alias (alias lmstudiorun='cd lmstudio/squashfs-root && ./lm-studio') to navigate to squashfs and run the program whne i type "lmstudiorun" in the terminal
  
4. Deployed AI service VM using template
5. Installed Docker and dependencies
6. Configured networking between VMs
7. Deployed AI services via Docker Compose

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
