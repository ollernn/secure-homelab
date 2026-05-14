# 05 - Security

## Security Overview

This document describes the basic security measures applied in the Secure Homelab project.

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

## Applied Security Measures

| Security Measure | Purpose | Status |
|---|---|---|
| Non-root user | Avoid using root for daily administration | Applied |
| SSH access | Manage the server remotely | Applied |
| SSH key authentication | Safer login method than password-only access | Applied |
| Disable root SSH login | Reduce risk of direct root access | Applied |
| Disable password login for SSH | Reduce brute-force risk | Applied |
| UFW firewall | Control open ports | Applied |
| Allow only required ports | Reduce attack surface | Applied |
| fail2ban | Protect against repeated failed login attempts | Applied |
| System updates | Keep system patched | Applied |
| Document open ports | Keep track of exposed services | Applied |

## SSH Security

SSH is used to manage the server from the Windows host machine.

The SSH key pair was created on the Windows host using:

```powershell
ssh-keygen
```

The public key was copied to the Ubuntu server with:

```powershell
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh -p 2222 olle@127.0.0.1 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

The SSH directory permissions were configured with:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

A custom SSH hardening configuration was created:

```bash
sudo nano /etc/ssh/sshd_config.d/99-secure-homelab.conf
```

Configuration:

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

## cloud-init SSH Configuration Issue

After applying the custom SSH configuration, `PasswordAuthentication` was still enabled.

This was checked with:

```bash
sudo sshd -T | grep -E "permitrootlogin|passwordauthentication|pubkeyauthentication"
```

Initial result:

```text
permitrootlogin no
pubkeyauthentication yes
passwordauthentication yes
```

The cause was another configuration file created by cloud-init:

```text
/etc/ssh/sshd_config.d/50-cloud-init.conf
```

It contained:

```text
PasswordAuthentication yes
```

This was changed to:

```text
PasswordAuthentication no
```

After restarting SSH, the final verified configuration was:

```text
permitrootlogin no
passwordauthentication no
pubkeyauthentication yes
```

## SSH Service Validation

The SSH configuration was tested before restarting the service:

```bash
sudo sshd -t
```

No errors were returned.

SSH was restarted with:

```bash
sudo systemctl restart ssh
```

A new SSH session was opened from Windows to confirm that access still worked:

```powershell
ssh -p 2222 olle@127.0.0.1
```

The login worked without a password, using SSH key authentication.

## Firewall Configuration

UFW is used as the basic firewall.

Initial status:

```bash
sudo ufw status
```

Result:

```text
Status: inactive
```

OpenSSH was allowed before enabling the firewall:

```bash
sudo ufw allow OpenSSH
```

The firewall was enabled with:

```bash
sudo ufw enable
```

The final firewall status was checked with:

```bash
sudo ufw status verbose
```

Result:

```text
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)

To                         Action      From
--                         ------      ----
22/tcp (OpenSSH)           ALLOW IN    Anywhere
22/tcp (OpenSSH (v6))      ALLOW IN    Anywhere (v6)
```

Portainer was later allowed through UFW with:

```bash
sudo ufw allow 9443/tcp
```

The firewall status was checked with:

```bash
sudo ufw status verbose
```

Result:

```text
22/tcp (OpenSSH)           ALLOW IN    Anywhere
9443/tcp                   ALLOW IN    Anywhere
22/tcp (OpenSSH (v6))      ALLOW IN    Anywhere (v6)
9443/tcp (v6)              ALLOW IN    Anywhere (v6)
```

Uptime Kuma was later allowed through UFW with:

```bash
sudo ufw allow 3001/tcp
```

Homepage was later allowed through UFW with:

```bash
sudo ufw allow 3000/tcp
```

Nginx was later allowed through UFW with:

```bash
sudo ufw allow 8080/tcp
```

The firewall now allows SSH, Portainer, Uptime Kuma, Homepage and Nginx.

## Open Ports

| Port | Service | Reason | Status |
|---:|---|---|---|
| 22 | SSH | Server administration | Allowed |
| 9443 | Portainer | Docker management web interface | Allowed |
| 3001 | Uptime Kuma | Monitoring dashboard | Allowed |
| 3000 | Homepage | Internal homelab dashboard | Allowed |
| 8080 | Nginx | Test web server | Allowed |
| 80 | HTTP / Nginx | Default web access later | Not opened yet |
| 443 | HTTPS / Nginx | Secure web access later | Not opened yet |

## fail2ban

fail2ban was installed to protect against repeated failed login attempts.

Installation command:

```bash
sudo apt install fail2ban -y
```

The service status was checked with:

```bash
sudo systemctl status fail2ban
```

Result:

```text
fail2ban.service - Fail2Ban Service
Active: active (running)
```

fail2ban is enabled and running.

## Security Decisions

| Decision | Reason |
|---|---|
| No public internet exposure in version 1 | Reduces risk while learning |
| Internal-only services | Management tools should not be publicly accessible |
| Use UFW instead of advanced firewall setup | Simple and suitable for version 1 |
| Allow only OpenSSH at this stage | Reduces exposed services |
| Use fail2ban | Adds protection against repeated failed login attempts |
| Use SSH keys | More secure than password-only login |
| Disable SSH password login | Reduces brute-force risk |
| Disable root SSH login | Prevents direct root access over SSH |

## Security Status

Status: Basic security configured

The server now uses SSH key authentication, root SSH login is disabled, password login over SSH is disabled, UFW is active and fail2ban is running.

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
