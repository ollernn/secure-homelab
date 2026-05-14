# 01 - Project Overview

## Project Purpose

The purpose of this project is to build a secure and documented homelab environment for learning practical infrastructure, Linux administration, containerization and cybersecurity.

Version 1 was built as a virtual machine on my main Windows PC using Oracle VirtualBox. This made it possible to learn and test server administration without needing separate physical hardware from the beginning.

## What I Built

I built a small Linux-based server environment that includes:

- Ubuntu Server 26.04 LTS
- Secure SSH access
- SSH key authentication
- UFW firewall
- fail2ban
- Basic server hardening
- Docker and Docker Compose
- Internal Docker services
- Service monitoring
- Internal dashboard
- Documentation, diagrams and screenshots

The goal was not only to install tools, but also to understand how they work together in a small server environment.

## Why This Project Matters

This project helped me develop hands-on skills that are relevant for roles within:

- IT infrastructure
- Cloud engineering
- Cybersecurity
- DevOps
- Systems administration
- Technical support and operations

By building the environment myself, I practiced real technical tasks such as configuring Linux, securing remote access, managing containers, setting up monitoring and documenting system design.

## Version 1 Scope

Version 1 of the project includes:

- Ubuntu Server 26.04 LTS running in a virtual machine
- SSH access from my Windows PC
- SSH key authentication
- Disabled SSH password login
- Disabled root login over SSH
- UFW firewall
- fail2ban
- Docker
- Docker Compose
- Portainer
- Uptime Kuma
- Homepage
- Nginx
- Screenshots
- Architecture diagrams
- Technical documentation

## Version 1 Services

The following internal services were deployed in version 1:

| Service | Purpose |
|---|---|
| Portainer | Docker management interface |
| Uptime Kuma | Service monitoring |
| Homepage | Internal homelab dashboard |
| Nginx | Test web server |

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
- Automated backup strategy
- Production-grade HTTPS certificates

## Final Outcome

At the end of version 1, I have a working Linux server environment running in a VirtualBox virtual machine.

The server is secured with basic hardening measures, runs several internal Docker services and is documented clearly in this GitHub repository.

The project is also prepared for presentation on my personal portfolio website.

## Portfolio Purpose

This project is also used as part of my personal portfolio.

The GitHub repository contains the detailed technical documentation, while my personal website includes a shorter summary of the project, the technologies used, screenshots, diagrams and the main lessons learned.

## Version 1 Status

Status: Complete

Secure Homelab v1 is installed, secured, documented and running internal Docker services.
