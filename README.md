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

- created the vm on node 2
  
  set ram size, cpu cores, iso, storage and continue.
   Note: cpu must be set to "Host" and not the default setting in the vm hardware settings or else lmstudio will not run properly.
  
- set up pcie passthrough
  added vfio in cmdline with nano in node 2

![image_api](https://github.com/LukasM2077/AI_VM/blob/main/images/Screenshot%202026-06-24%20200802.png?raw=true)

---

  used VirtIO SCSI single and add the pci device

---

  ![image_api](https://github.com/LukasM2077/AI_VM/blob/main/images/Screenshot%202026-06-24%20200907.png?raw=true)

---

![image_api](https://github.com/LukasM2077/AI_VM/blob/main/images/screenshot2026.png?raw=true)

---

- installed LmStudio
   1. went to LmStudio's website and downloaded the linux appimage on the vm.
   2. created a folder for LmStudio (lmstudio) in home. Moved appimage to new folder.
   3. give appimage file permissions. cd into the folder and use chmod (chmod u+x LM-Studio-0.4.2.2-64x.AppImage)

![image_api](https://github.com/LukasM2077/AI_VM/blob/main/images/Screenshot%202026-06-24%20185809.png?raw=true)

   4. execute and extract appimage (./LM-Studio-0.4.2.2-64x.AppImage --appimage-extract
    5. enter the new folder squashfs-root
    6. set permissions in squashfs using (sudo chown root:root chrome-sandbox) and (sudo chmod 4755 chrome-sandbox)
    7. run the program (./lm-studio)

   8. Easy startup
instead of having to navigate to squashfs-root each time to run lmstudio, I created an alias (alias lmstudiorun='cd lmstudio/squashfs-root && ./lm-studio') to navigate to squashfs and run the program when i type "lmstudiorun" in the terminal

---
  
- Installed Docker
    Updated (sudo apt update && sudo apt upgrade -y) and Installed docker from their website and follow the instructions ( sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin)

![image_api](https://github.com/LukasM2077/AI_VM/blob/main/images/Screenshot%202026-06-24%20193211.png?raw=true)

- Installed anythingllm docker image
  
   used the pull command (docker pull mintplexlabs/anythingllm:latest) listed on their website

-installed Tailscale

  used (curl -fsSL https://tailscale.com/install.sh | sh) to install.

-used SOCAT for Tailscale

  used socat command (socat TCP-LISTEN:3001,fork,reuseaddr TCP:127.0.0.1:3001) so tailscale can see it, and i can access the image wile on my tailnet and outside of my home network.

- Set up anythingllm image
  
  using the website's command:

---

( export STORAGE_LOCATION=$HOME/anythingllm && \
mkdir -p $STORAGE_LOCATION && \
touch "$STORAGE_LOCATION/.env" && \
docker run -d -p 3001:3001 \
--cap-add SYS_ADMIN \
--name anythingllm \
-v ${STORAGE_LOCATION}:/app/server/storage \
-v ${STORAGE_LOCATION}/.env:/app/server/.env \
-e STORAGE_DIR="/app/server/storage" \
mintplexlabs/anythingllm  )

---

- set up anythingllm
  added docs, set up the model, and customized the app.

![image_api](https://github.com/LukasM2077/AI_VM/blob/main/images/Screenshot%202026-06-24%20200125.png?raw=true)
  
---

## Demonstration Of AI

![image_api](https://github.com/LukasM2077/AI_VM/blob/main/images/Screenshot%202026-06-24%20194717.png?raw=true)
  
## Networking

- Static IP assignment for VM
- Bridge networking via Proxmox (vmbr0)
- Tailscale
- socat

---

## services

- Docker https://docs.docker.com/engine/install/ubuntu/
- anythingllm https://docs.anythingllm.com/installation-docker/available-images
- lmstudio https://lmstudio.ai/download
- Tailscale https://tailscale.com/download/linux
  
## Skills Demonstrated

- Virtualization (Proxmox VE)
- Linux system administration
- Networking and IP management
- Docker and containerization
- Infrastructure documentation
- Basic AI service deployment
- PCIE passthrough and other tools
