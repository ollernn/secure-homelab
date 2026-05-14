# Secure Homelab

## Overview

Secure Homelab is a personal infrastructure and cybersecurity project where I build, secure and document a small server environment using Linux, SSH, firewall rules, Docker and internal services.

The purpose of the project is to develop practical skills in Linux administration, secure server configuration, containerization, monitoring and technical documentation.

## Goals

- Set up an Ubuntu Server virtual machine
- Configure secure SSH access
- Apply basic server hardening
- Install and use Docker and Docker Compose
- Run internal services such as Portainer, Uptime Kuma, Homepage and Nginx
- Document the environment clearly
- Create a portfolio-ready project with screenshots, diagrams and lessons learned

## Technologies

- Ubuntu Server 26.04 LTS
- SSH
- UFW Firewall
- fail2ban
- Docker
- Docker Compose
- Portainer
- Uptime Kuma
- Homepage
- Nginx
- GitHub

## Project Structure

```text
secure-homelab/
├── README.md
├── docs/
│   ├── 01-overview.md
│   ├── 02-hardware-and-vm.md
│   ├── 03-network.md
│   ├── 04-installation.md
│   ├── 05-security.md
│   ├── 06-docker-services.md
│   └── 07-lessons-learned.md
├── docker/
│   ├── portainer/
│   ├── uptime-kuma/
│   ├── homepage/
│   └── nginx/
├── diagrams/
└── screenshots/
```

## Current Status

Status: Internal services deployed

Ubuntu Server 26.04 LTS is installed in a VirtualBox virtual machine. SSH access is secured with key-based authentication, UFW is active, fail2ban is running, Docker with Docker Compose is installed, and the first internal services are deployed: Portainer, Uptime Kuma and Homepage.

## Completed So Far

- Created the GitHub repository and project structure
- Installed Ubuntu Server 26.04 LTS in VirtualBox
- Configured NAT networking with SSH port forwarding
- Tested SSH access from the Windows host
- Created and configured SSH key-based authentication
- Disabled root login over SSH
- Disabled password authentication over SSH
- Enabled and configured UFW firewall
- Installed and verified fail2ban
- Installed Docker and Docker Compose
- Verified Docker with the `hello-world` test container
- Documented installation, network setup, security configuration and Docker setup
- Deployed Portainer as a Docker management interface
- Deployed Uptime Kuma for service monitoring
- Deployed Homepage as an internal homelab dashboard
- Added Portainer and Homepage as monitored services in Uptime Kuma

## Version 1 Scope

The first version of the homelab includes:

- Ubuntu Server running in a virtual machine
- SSH access from my Windows PC
- SSH key authentication
- Basic Linux configuration
- UFW firewall
- fail2ban
- Docker
- Docker Compose
- Portainer
- Uptime Kuma
- Homepage
- Nginx
- Basic documentation, screenshots and diagrams

## Not Included in Version 1

The following parts are intentionally left for later versions:

- Dedicated physical server
- VLAN segmentation
- VPN access
- Public exposure to the internet
- Kubernetes
- Terraform
- Azure integration
- SIEM or advanced security monitoring

## Documentation

Detailed documentation is available in the `docs/` folder:

- `01-overview.md` - Project overview and purpose
- `02-hardware-and-vm.md` - Host machine and virtual machine setup
- `03-network.md` - Network setup, NAT and SSH port forwarding
- `04-installation.md` - Ubuntu Server installation and setup
- `05-security.md` - SSH hardening, UFW and fail2ban
- `06-docker-services.md` - Docker installation and planned services
- `07-lessons-learned.md` - Reflections, problems and lessons learned

## Next Steps

1. Deploy Nginx as a web server / reverse proxy
2. Add Nginx to Homepage
3. Add Nginx to Uptime Kuma monitoring
4. Document service configuration, ports and screenshots
5. Create a portfolio summary on my personal website

## Purpose of the Portfolio Version

The website version of this project will provide a shorter summary of the homelab, including what was built, why it was built, which technologies were used and what I learned.

The GitHub repository contains the more detailed technical documentation.
