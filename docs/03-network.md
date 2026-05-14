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

## Network Decision for Version 1

For the first version, the project uses NAT networking.

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

SSH access was tested from the Windows host using Windows Terminal / PowerShell.

The first attempt was made directly to the VM NAT address:

```bash
ssh olle@10.0.2.15
```

This resulted in a timeout because the VM was running behind VirtualBox NAT.

To solve this, a VirtualBox port forwarding rule was created.

| Setting | Value |
|---|---|
| Name | SSH |
| Protocol | TCP |
| Host IP | 127.0.0.1 |
| Host Port | 2222 |
| Guest IP | empty |
| Guest Port | 22 |

After adding the port forwarding rule, SSH access worked with:

```bash
ssh -p 2222 olle@127.0.0.1
```

Result:

```text
SSH connection successful
```

This allows the Ubuntu Server VM to be managed from the Windows host without using the VirtualBox console.

After SSH key authentication was configured, password login over SSH was disabled.

The current SSH access method is:

```bash
ssh -p 2222 olle@127.0.0.1
```

Authentication is done with the SSH key stored on the Windows host.

## Portainer Access

Portainer is accessed through HTTPS on port `9443`.

Because the VM uses VirtualBox NAT, a port forwarding rule is used from the Windows host to the Ubuntu VM.

| Setting | Value |
|---|---|
| Name | Portainer |
| Protocol | TCP |
| Host IP | 127.0.0.1 |
| Host Port | 9443 |
| Guest IP | empty |
| Guest Port | 9443 |

Access URL from the Windows host:

```text
https://127.0.0.1:9443
```

Portainer uses a self-signed certificate in this internal lab environment.

## Uptime Kuma Access

Uptime Kuma is accessed through HTTP on port `3001`.

Because the VM uses VirtualBox NAT, a port forwarding rule is used from the Windows host to the Ubuntu VM.

| Setting | Value |
|---|---|
| Name | Uptime Kuma |
| Protocol | TCP |
| Host IP | 127.0.0.1 |
| Host Port | 3001 |
| Guest IP | empty |
| Guest Port | 3001 |

Access URL from the Windows host:

```text
http://127.0.0.1:3001
```

## Homepage Access

Homepage is accessed through HTTP on port `3000`.

Because the VM uses VirtualBox NAT, a port forwarding rule is used from the Windows host to the Ubuntu VM.

| Setting | Value |
|---|---|
| Name | Homepage |
| Protocol | TCP |
| Host IP | 127.0.0.1 |
| Host Port | 3000 |
| Guest IP | empty |
| Guest Port | 3000 |

Access URL from the Windows host:

```text
http://127.0.0.1:3000
```

## Nginx Access

Nginx is accessed through HTTP on port `8080`.

Because the VM uses VirtualBox NAT, a port forwarding rule is used from the Windows host to the Ubuntu VM.

| Setting | Value |
|---|---|
| Name | Nginx |
| Protocol | TCP |
| Host IP | 127.0.0.1 |
| Host Port | 8080 |
| Guest IP | empty |
| Guest Port | 8080 |

Access URL from the Windows host:

```text
http://127.0.0.1:8080
```

## Docker Internal Networking

A custom Docker network named `homelab` was created so that containers can communicate with each other by container name.

The network was created with:

```bash
docker network create homelab
```

The following containers were connected to the `homelab` network:

- `portainer`
- `uptime-kuma`
- `homepage`
- `nginx`

This allows Uptime Kuma to monitor Portainer with:

```text
https://portainer:9443
```

Using `https://127.0.0.1:9443` inside Uptime Kuma did not work, because `127.0.0.1` inside a container refers to the container itself.

This allows Uptime Kuma to monitor Homepage with:

```text
http://homepage:3000
```

This allows Uptime Kuma to monitor Nginx with:

```text
http://nginx:80
```

## Planned Internal Services

The following services are planned for version 1:

| Service | Purpose | Access |
|---|---|---|
| Portainer | Docker management | Internal only |
| Uptime Kuma | Monitoring | Internal only |
| Homepage | Homelab dashboard | Internal only |
| Nginx | Web server / reverse proxy | Internal only |

## Ports

| Port | Service | Notes | Status |
|---:|---|---|---|
| 22 | SSH | Used for server administration | Allowed in UFW |
| 9443 | Portainer | Docker management web interface | Allowed in UFW |
| 3001 | Uptime Kuma | Monitoring dashboard | Allowed in UFW |
| 3000 | Homepage | Internal homelab dashboard | Allowed in UFW |
| 8080 | Nginx | Test web server | Allowed in UFW |
| 80 | HTTP / Nginx | Default HTTP port, not used directly yet | Not opened yet |
| 443 | HTTPS / Nginx | May be used later | Not opened yet |
| 9000 | Portainer HTTP | Exposed by container but not used directly | Not opened in UFW |

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
