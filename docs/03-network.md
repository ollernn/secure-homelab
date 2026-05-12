# 03 - Network

## Network Overview

The first version of the homelab will run as a virtual machine on my main Windows PC.

The virtual machine will use the host computer's network connection to access the internet and communicate with the host machine.

## Basic Network Structure

```text
Internet
   |
Home Router
   |
Windows Host PC
   |
Virtual Machine
   |
Ubuntu Server
   |
Docker Services
```

## Network Mode

The virtual machine currently uses NAT networking.

NAT is a good starting point because it allows the Ubuntu Server VM to access the internet through the host computer without exposing the server directly to the rest of the network.

## NAT Networking

With NAT networking, the virtual machine can:

- access the internet
- download updates
- install packages
- communicate through the host computer's network connection

However, other devices on the home network may not be able to access the VM directly without extra configuration.

## Bridged Networking

Bridged networking may be used later if the server needs to behave more like a separate physical device on the home network.

With bridged networking, the VM gets its own IP address from the home router.

This makes it easier to access services from other devices on the same network.

## Planned Network Decision for Version 1

For the first version, the project will start with NAT networking.

Bridged networking may be tested later if needed.

| Network Mode | Used in Version 1? | Reason |
|---|---|---|
| NAT | Yes | Simple and safer starting point |
| Bridged | Later if needed | Useful when accessing services from other devices |
| Public internet exposure | No | Not needed for version 1 |

## IP Address

The server IP address was checked after the Ubuntu Server installation.

Commands used:

```bash
hostname -I
```

```bash
ip a
```

The command `hostname -i` returned:

```text
127.0.1.1
```

This is a local hostname address and should not be used for SSH access.

The correct IPv4 address was found under the `enp0s3` network interface:

| Field | Value |
|---|---|
| Interface | enp0s3 |
| IPv4 address | 10.0.2.15 |
| Network mode | NAT |

## SSH Access

The goal is to access the Ubuntu Server VM from the Windows host using SSH.

Planned SSH command from Windows Terminal:

```bash
ssh olle@10.0.2.15
```

SSH was installed during the Ubuntu Server installation.

SSH access will be tested in the next step.

## Planned Internal Services

The following services are planned for version 1:

| Service | Purpose | Access |
|---|---|---|
| Portainer | Docker management | Internal only |
| Uptime Kuma | Monitoring | Internal only |
| Homepage | Homelab dashboard | Internal only |
| Nginx | Web server / reverse proxy | Internal only |

## Planned Ports

The exact ports may change during implementation, but the expected ports are:

| Port | Service | Notes |
|---:|---|---|
| 22 | SSH | Used for server administration |
| 80 | HTTP / Nginx | Used for web access |
| 443 | HTTPS / Nginx | May be used later |
| 9000 | Portainer | Docker management interface |
| 3001 | Uptime Kuma | Monitoring dashboard |

## Security Considerations

The first version of the homelab will not be exposed directly to the public internet.

All services will be used internally for learning, testing and documentation.

Security measures will include:

- UFW firewall
- SSH hardening
- fail2ban
- limited open ports
- internal-only access to management services

## Future Network Improvements

Future versions of the homelab may include:

- Bridged networking
- Static IP address
- Dedicated physical server
- VLAN segmentation
- Separate network for servers
- VPN access
- Reverse proxy with HTTPS
- More advanced monitoring and logging

## Version 1 Network Summary

For version 1, the homelab will use a simple and safe network setup.

The Ubuntu Server VM currently uses NAT networking, internal services and no public internet exposure.

More advanced networking will be added later when the basic server environment is working.
