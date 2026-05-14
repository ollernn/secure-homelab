# 08 - Version 1 Summary

## Overview

Secure Homelab v1 is a personal infrastructure and cybersecurity project where a small server environment was built, secured and documented.

The project was built using Ubuntu Server 26.04 LTS inside a VirtualBox virtual machine on a Windows host machine. The goal was to create a practical learning environment for Linux administration, SSH, firewall configuration, Docker, monitoring and technical documentation.

## Purpose

The purpose of version 1 was to build a secure and functional foundation for a homelab environment.

The project was designed to improve practical skills in:

- Linux server administration
- Secure remote access with SSH
- Firewall configuration
- Basic server hardening
- Docker and Docker Compose
- Container-based services
- Service monitoring
- Technical documentation
- Portfolio project presentation

## Final Version 1 Architecture

The final version 1 setup includes:

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
   |
Shared Docker Network: homelab
   |-- Portainer
   |-- Uptime Kuma
   |-- Homepage
   |-- Nginx
```

## Main Components

| Component | Purpose |
|---|---|
| Windows Host PC | Runs VirtualBox and accesses services through forwarded ports |
| Oracle VirtualBox | Runs the Ubuntu Server virtual machine |
| Ubuntu Server 26.04 LTS | Main server operating system |
| SSH | Remote server administration |
| UFW | Firewall for controlling allowed ports |
| fail2ban | Protection against repeated failed login attempts |
| Docker | Runs internal services as containers |
| Docker Compose | Defines and starts services using YAML files |
| Portainer | Docker management interface |
| Uptime Kuma | Service monitoring |
| Homepage | Internal dashboard for homelab links |
| Nginx | Test web server |

## Virtual Machine Configuration

| Setting | Value |
|---|---|
| VM name | secure-homelab |
| Operating system | Ubuntu Server 26.04 LTS |
| Virtualization platform | Oracle VirtualBox |
| RAM | 4096 MB |
| CPU | 2 cores |
| Disk | 80 GB |
| Network mode | NAT |
| Hostname | secure-homelab |
| Local user | olle |

## Network and Port Forwarding

Because the VM uses VirtualBox NAT, port forwarding is used to access services from the Windows host.

| Host Address | Guest Service | Purpose |
|---|---|---|
| `127.0.0.1:2222` | `22` | SSH |
| `127.0.0.1:9443` | `9443` | Portainer |
| `127.0.0.1:3001` | `3001` | Uptime Kuma |
| `127.0.0.1:3000` | `3000` | Homepage |
| `127.0.0.1:8080` | `8080 → 80` | Nginx |

## Security Configuration

Version 1 includes basic server hardening.

The following security measures were applied:

- SSH key authentication configured
- Password authentication over SSH disabled
- Root login over SSH disabled
- UFW firewall enabled
- Only required ports allowed
- fail2ban installed and running
- Server updated after installation
- No public internet exposure configured
- Portainer kept internal because it has access to the Docker socket

Final verified SSH settings:

```text
permitrootlogin no
passwordauthentication no
pubkeyauthentication yes
```

## Firewall Rules

UFW was configured to allow only the required ports for version 1.

| Port | Service | Status |
|---:|---|---|
| 22 | SSH | Allowed |
| 9443 | Portainer | Allowed |
| 3001 | Uptime Kuma | Allowed |
| 3000 | Homepage | Allowed |
| 8080 | Nginx | Allowed |

## Docker Services

The following Docker services were deployed in version 1:

| Service | Port | Purpose | Status |
|---|---:|---|---|
| Portainer | 9443 | Docker management | Running |
| Uptime Kuma | 3001 | Monitoring | Running |
| Homepage | 3000 | Internal dashboard | Running |
| Nginx | 8080 → 80 | Test web server | Running |

## Monitoring

Uptime Kuma was configured to monitor internal services.

Monitored services:

- Portainer
- Homepage
- Nginx

```markdown
The services are monitored internally using Docker container names on the shared Docker network:

| Service | Internal monitoring URL |
|---|---|
| Portainer | `https://portainer:9443` |
| Homepage | `http://homepage:3000` |
| Nginx | `http://nginx:80` |
```

This was an important learning point because `127.0.0.1` inside a container refers to the container itself, not the Windows host or another container.

## Homepage Dashboard

Homepage was configured as an internal dashboard for the homelab.

The dashboard includes links to:

- Portainer
- Uptime Kuma
- Nginx

Homepage makes the homelab easier to navigate and provides a simple visual overview of the deployed services.

## Nginx Test Web Server

Nginx was deployed as a simple test web server.

A custom HTML page was created and served from the Ubuntu Server VM through Docker.

Access URL:

```text
http://127.0.0.1:8080
```

## Problems Solved

Several problems were encountered and solved during version 1.

| Problem | Cause | Solution |
|---|---|---|
| SSH to `10.0.2.15` timed out | VirtualBox NAT did not expose the VM SSH port directly | Added port forwarding from `127.0.0.1:2222` to guest port `22` |
| `hostname -i` showed `127.0.1.1` | Local hostname address, not the VM network address | Used `ip a` to find the real interface IP |
| `PasswordAuthentication no` did not apply at first | cloud-init file overrode SSH configuration | Changed `/etc/ssh/sshd_config.d/50-cloud-init.conf` |
| Uptime Kuma could not monitor Portainer through `127.0.0.1` | `127.0.0.1` inside a container refers to itself | Created a shared Docker network and used `https://portainer:9443` |
| Portainer used a self-signed certificate | Default internal HTTPS certificate | Ignored TLS/SSL errors for the internal Uptime Kuma monitor |

## Screenshots

Screenshots are stored in the `screenshots/` folder.

Screenshots included for version 1:

| Screenshot | Purpose |
|---|---|
| VirtualBox overview | Shows VM configuration |
| SSH access | Shows remote administration |
| UFW firewall status | Shows firewall configuration |
| Docker containers | Shows running services |
| Portainer dashboard | Shows Docker management |
| Uptime Kuma monitoring | Shows service monitoring |
| Homepage dashboard | Shows internal dashboard |
| Nginx test page | Shows web server output |

## Diagrams

Architecture diagrams are stored in the `diagrams/` folder.

Version 1 includes:

- Simple architecture diagram
- Detailed architecture diagram

The simple diagram is intended for portfolio presentation.

The detailed diagram is intended for technical GitHub documentation.

## What I Learned

During version 1, I learned how to:

- Install Ubuntu Server in a virtual machine
- Configure and access a Linux server through SSH
- Use SSH keys for secure authentication
- Harden SSH by disabling root and password login
- Configure UFW firewall rules
- Install and verify fail2ban
- Install Docker and Docker Compose
- Run services as Docker containers
- Use Docker volumes for persistent data
- Use Docker networks for container-to-container communication
- Deploy Portainer, Uptime Kuma, Homepage and Nginx
- Monitor services with Uptime Kuma
- Create technical documentation in GitHub
- Prepare a project for portfolio presentation

## Version 1 Status

Status: Complete

Secure Homelab v1 is installed, secured, documented and running internal Docker services.

## Next Steps for Version 2

Possible improvements for version 2:

- Move from VirtualBox VM to a dedicated mini-PC server
- Add reverse proxy configuration with Nginx
- Add HTTPS with trusted certificates
- Add backups for Docker volumes and configuration files
- Add automated update strategy
- Improve Homepage dashboard design
- Add more monitoring targets
- Add centralized logging
- Add VPN access
- Add VLAN/network segmentation
- Add cloud integration later
- Improve documentation as the homelab evolves
