# Secure Homelab

## Overview

Secure Homelab is a personal infrastructure and cybersecurity project where I build, secure and document a small server environment using Linux, SSH, firewall rules, Docker and internal services.

The purpose of the project is to develop practical skills in Linux administration, secure server configuration, containerization, monitoring, service management and technical documentation.

Version 1 is built as a virtual machine on my Windows PC using Oracle VirtualBox.

## Project Goals

The main goals of this project are to:

- Set up an Ubuntu Server virtual machine
- Configure secure SSH access
- Apply basic server hardening
- Configure firewall rules
- Install and use Docker and Docker Compose
- Deploy internal services with Docker
- Monitor services with Uptime Kuma
- Create an internal homelab dashboard
- Document the environment clearly
- Create a portfolio-ready infrastructure project

## Technologies Used

- Ubuntu Server 26.04 LTS
- Oracle VirtualBox
- SSH
- SSH key authentication
- UFW Firewall
- fail2ban
- Docker
- Docker Compose
- Portainer
- Uptime Kuma
- Homepage
- Nginx
- GitHub
- Mermaid diagrams

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
│   ├── 07-lessons-learned.md
│   └── 08-version-1-summary.md
├── docker/
│   ├── portainer/
│   ├── uptime-kuma/
│   ├── homepage/
│   └── nginx/
├── diagrams/
│   ├── secure-homelab-v1-simple.md
│   └── secure-homelab-v1-detailed.md
└── screenshots/
    ├── 01-virtualbox-vm-overview.png
    ├── 02-ssh-access.png
    ├── 03-ufw-firewall-status.png
    ├── 04-docker-containers.png
    ├── 05-portainer-dashboard.png
    ├── 06-uptime-kuma-monitoring.png
    ├── 07-homepage-dashboard.png
    └── 08-nginx-test-page.png
```

## Current Status

Status: Version 1 complete

Ubuntu Server 26.04 LTS is installed in a VirtualBox virtual machine. SSH access is secured with key-based authentication, UFW is active, fail2ban is running, Docker with Docker Compose is installed, and the first internal services are deployed: Portainer, Uptime Kuma, Homepage and Nginx.

The project is documented with technical notes, screenshots, architecture diagrams and a version 1 summary.

## Version 1 Architecture

Version 1 uses the following structure:

```text
Windows Host PC
   |
Oracle VirtualBox
   |
Ubuntu Server 26.04 LTS VM
   |
Security Layer
   |-- SSH key authentication
   |-- UFW firewall
   |-- fail2ban
   |
Docker Engine
   |-- Portainer
   |-- Uptime Kuma
   |-- Homepage
   |-- Nginx
```

## Virtual Machine Configuration

| Setting | Value |
|---|---|
| VM name | secure-homelab |
| Operating system | Ubuntu Server 26.04 LTS |
| Virtualization | Oracle VirtualBox |
| RAM | 4096 MB |
| CPU | 2 cores |
| Disk | 80 GB |
| Network mode | NAT |
| Hostname | secure-homelab |

## Network Access

The virtual machine uses VirtualBox NAT networking. Services are accessed from the Windows host using port forwarding.

| Host Address | Guest Service | Purpose |
|---|---|---|
| `127.0.0.1:2222` | `22` | SSH |
| `127.0.0.1:9443` | `9443` | Portainer |
| `127.0.0.1:3001` | `3001` | Uptime Kuma |
| `127.0.0.1:3000` | `3000` | Homepage |
| `127.0.0.1:8080` | `80` | Nginx |

## Security Configuration

Basic server hardening has been applied.

Security measures include:

- SSH key authentication
- Disabled root login over SSH
- Disabled password authentication over SSH
- UFW firewall enabled
- Only required ports allowed
- fail2ban installed and running
- No public internet exposure configured

Final verified SSH settings:

```text
permitrootlogin no
passwordauthentication no
pubkeyauthentication yes
```

## Deployed Services

| Service | Purpose | Access |
|---|---|---|
| Portainer | Docker management interface | `https://127.0.0.1:9443` |
| Uptime Kuma | Service monitoring | `http://127.0.0.1:3001` |
| Homepage | Internal homelab dashboard | `http://127.0.0.1:3000` |
| Nginx | Test web server | `http://127.0.0.1:8080` |

## Monitoring

Uptime Kuma is used to monitor internal services.

Monitored services:

- Portainer
- Homepage
- Nginx

The services are monitored through a shared Docker network using container names.

Examples:

```text
https://portainer:9443
http://homepage:3000
http://nginx:80
```

## Completed in Version 1

- Created the GitHub repository and project structure
- Installed Ubuntu Server 26.04 LTS in VirtualBox
- Configured NAT networking with port forwarding
- Tested SSH access from the Windows host
- Created and configured SSH key-based authentication
- Disabled root login over SSH
- Disabled password authentication over SSH
- Enabled and configured UFW firewall
- Installed and verified fail2ban
- Installed Docker and Docker Compose
- Verified Docker with the `hello-world` test container
- Deployed Portainer as a Docker management interface
- Deployed Uptime Kuma for service monitoring
- Deployed Homepage as an internal homelab dashboard
- Deployed Nginx as a test web server
- Added Portainer, Homepage and Nginx to Uptime Kuma monitoring
- Added Portainer, Uptime Kuma and Nginx to Homepage
- Created screenshots for documentation
- Created simple and detailed architecture diagrams
- Created a final version 1 summary

## Documentation

Detailed documentation is available in the `docs/` folder:

- `01-overview.md` - Project overview and purpose
- `02-hardware-and-vm.md` - Host machine and virtual machine setup
- `03-network.md` - Network setup, NAT, port forwarding and Docker networking
- `04-installation.md` - Ubuntu Server installation and setup
- `05-security.md` - SSH hardening, UFW and fail2ban
- `06-docker-services.md` - Docker installation and deployed services
- `07-lessons-learned.md` - Reflections, problems and lessons learned
- `08-version-1-summary.md` - Final version 1 summary

## Diagrams

Architecture diagrams are available in the `diagrams/` folder:

- `secure-homelab-v1-simple.md` - Simple diagram for portfolio presentation
- `secure-homelab-v1-detailed.md` - Detailed technical diagram for GitHub documentation

## Screenshots

Screenshots are available in the `screenshots/` folder.

They show:

- VirtualBox VM overview
- SSH access from Windows
- UFW firewall status
- Running Docker containers
- Portainer dashboard
- Uptime Kuma monitoring
- Homepage dashboard
- Nginx test page

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
- Automated backups
- Production-grade HTTPS certificates

## Future Improvements

Possible improvements for version 2:

- Move the homelab from VirtualBox to a dedicated mini-PC server
- Configure Nginx as a reverse proxy
- Add HTTPS with trusted certificates
- Add backup strategy for Docker volumes and configuration files
- Improve Homepage with icons, widgets and service status
- Add more monitoring targets
- Add centralized logging
- Add VPN access
- Add VLAN or network segmentation
- Add cloud integration later

## Portfolio Purpose

This project is also used as part of my personal portfolio.

The GitHub repository contains the detailed technical documentation, while my personal website presents a shorter summary of the project, the technologies used, screenshots, diagrams and the main lessons learned.
