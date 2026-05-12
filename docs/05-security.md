# 05 - Security

## Security Overview

This document describes the basic security measures planned and applied in the Secure Homelab project.

The goal is to create a safer Linux server environment before installing and exposing internal services.

Version 1 focuses on basic server hardening, secure remote access and limited network exposure.

## Security Goals

The main security goals for version 1 are:

- Use secure SSH access
- Disable unnecessary access methods
- Limit open ports
- Enable a firewall
- Protect against repeated login attempts
- Keep the server updated
- Document all security decisions

## Threat Model

The first version of the homelab is not exposed to the public internet.

The main risks for version 1 are:

- Weak SSH configuration
- Unnecessary open ports
- Misconfigured services
- Outdated packages
- Poor password or user management
- Accidental exposure of management interfaces

The goal is not to create enterprise-level security, but to build a secure foundation for learning and future improvements.

## Planned Security Measures

| Security Measure | Purpose | Status |
|---|---|---|
| Create a non-root user | Avoid using root for daily administration | Planned |
| Use SSH access | Manage the server remotely | Planned |
| Use SSH keys | Safer login method than password-only access | Planned |
| Disable root SSH login | Reduce risk of direct root access | Planned |
| Disable password login for SSH | Reduce brute-force risk | Planned |
| Enable UFW firewall | Control open ports | Planned |
| Allow only required ports | Reduce attack surface | Planned |
| Install fail2ban | Block repeated failed login attempts | Planned |
| Enable automatic security updates | Keep system patched | Planned |
| Document open ports | Keep track of exposed services | Planned |

## SSH Security

SSH will be used to manage the server from the Windows host machine.

Planned SSH hardening:

- Use SSH keys
- Disable root login
- Disable password authentication after SSH keys are working
- Only allow SSH from the internal environment
- Keep SSH access internal only

Planned SSH configuration file:

```text
/etc/ssh/sshd_config
```

Planned settings to review:

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

The exact configuration will be updated after implementation.

## Firewall Configuration

UFW will be used as the basic firewall.

Planned default rules:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

Planned allowed services:

```bash
sudo ufw allow OpenSSH
```

Other ports will only be opened when needed.

## Planned Open Ports

| Port | Service | Reason | Status |
|---:|---|---|---|
| 22 | SSH | Server administration | Planned |
| 80 | HTTP / Nginx | Web access later | Planned |
| 443 | HTTPS / Nginx | Secure web access later | Future |
| 9000 | Portainer | Docker management | Planned/internal only |
| 3001 | Uptime Kuma | Monitoring dashboard | Planned/internal only |

The final list of open ports will be updated after the services are installed.

## fail2ban

fail2ban will be installed to protect against repeated failed login attempts.

Planned installation:

```bash
sudo apt install fail2ban -y
```

Planned service check:

```bash
sudo systemctl status fail2ban
```

The exact configuration will be documented after implementation.

## Automatic Security Updates

Automatic security updates will be enabled to keep the server patched.

Planned package:

```bash
sudo apt install unattended-upgrades -y
```

Planned configuration command:

```bash
sudo dpkg-reconfigure unattended-upgrades
```

## Update Routine

The server should be updated regularly.

Manual update commands:

```bash
sudo apt update
sudo apt upgrade -y
```

## Security Decisions

| Decision | Reason |
|---|---|
| No public internet exposure in version 1 | Reduces risk while learning |
| Internal-only services | Management tools should not be publicly accessible |
| Use UFW instead of advanced firewall setup | Simple and suitable for version 1 |
| Use fail2ban | Adds protection against repeated failed login attempts |
| Use SSH keys | More secure than password-only login |

## Security Status

Status: Planned

The security configuration has not been applied yet.

This document will be updated after SSH, UFW, fail2ban and automatic updates have been configured.

## Future Security Improvements

Future versions may include:

- VPN access
- VLAN segmentation
- Centralized logging
- Reverse proxy with HTTPS
- More advanced monitoring
- SIEM integration
- IDS/IPS
- Backup strategy
- Secrets management
