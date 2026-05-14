# 02 - Hardware and Virtual Machine

## Host Machine

Secure Homelab v1 is built on my main Windows PC.

This means that the server environment runs inside a virtual machine instead of on separate physical server hardware.

The purpose of this setup is to create a practical Linux server environment where I can build, secure, run and document server services locally.

## Host Specifications

| Component | Specification |
|---|---|
| CPU | AMD Ryzen 5 5600X / 6-Core Processor |
| RAM | 32 GB |
| GPU | NVIDIA GeForce RTX 3060 Ti, 8 GB |
| Storage | 2.27 TB |
| Host Operating System | Windows |

## Virtualization Platform

The virtual machine is created and managed using Oracle VirtualBox.

VirtualBox is used because it makes it possible to run a separate Linux server environment on my existing Windows computer without needing additional physical hardware.

This is useful for the first version of the project because the server can be started, stopped, rebuilt and documented in a controlled way.

## Why I Am Using a Virtual Machine

Version 1 of this project is built in a virtual machine.

This is a good starting point because it allows me to build and test a server environment without buying separate hardware at the beginning of the project.

A virtual machine also makes the lab easier to manage. It can be started when I want to work on the project and shut down when I want to use my main computer normally.

## Benefits of Using a Virtual Machine

Using a virtual machine has several advantages:

- No extra hardware is required
- The lab can be started and stopped when needed
- The host computer is only affected while the VM is running
- The environment is easier to rebuild if something goes wrong
- It is a safe way to learn Linux server administration
- It makes the first version of the project cheaper and easier to start
- It provides a controlled environment for testing security settings and services

## Virtual Machine Configuration

The virtual machine has been configured with enough resources to run Ubuntu Server, Docker and the internal services used in Secure Homelab v1.

| Setting | Value |
|---|---|
| VM Name | `secure-homelab` |
| Hostname | `secure-homelab` |
| Local user | `olle` |
| Operating System | Ubuntu Server 26.04 LTS |
| RAM | 4096 MB |
| CPU | 2 cores |
| Disk | 80 GB |
| Network Mode | NAT |

## Operating System Verification

The virtual machine runs Ubuntu Server 26.04 LTS.

The installed Ubuntu version was verified inside the server using the `lsb_release -a` command.

This confirmed that the installed operating system is Ubuntu Server 26.04 LTS.

VirtualBox may display the guest operating system type as Ubuntu 25.04, but the actual installed server version has been verified from inside Ubuntu.

## Why These Resources Are Enough

The virtual machine has enough resources to run Ubuntu Server, Docker and the internal services used in Secure Homelab v1.

The current services are:

- Portainer
- Uptime Kuma
- Homepage
- Nginx

These services do not require a powerful server. The allocated VM resources are enough for learning, testing, monitoring and documentation.

Because the host computer has 32 GB of RAM and a 6-core processor, it can run the VM while still having enough resources left for normal use.

## Network Mode

The VM uses NAT networking in VirtualBox.

This means that the virtual machine is isolated behind the host computer instead of being directly exposed on the local network.

Because NAT is used, VirtualBox port forwarding is configured so that selected services inside the VM can be accessed from the Windows host.

The forwarded services are:

| Host Address | Guest Service | Purpose |
|---|---|---|
| `127.0.0.1:2222` | `22` | SSH |
| `127.0.0.1:9443` | `9443` | Portainer |
| `127.0.0.1:3001` | `3001` | Uptime Kuma |
| `127.0.0.1:3000` | `3000` | Homepage |
| `127.0.0.1:8080` | `80` | Nginx |

## Performance Impact

The host computer is mainly affected when the virtual machine is running.

When the VM is turned off, it does not use CPU or RAM. It only takes up disk space.

This makes it possible to use the main computer normally when the homelab is not active.

## Future Hardware Plan

If the homelab grows, it may later be moved to a dedicated mini-PC server.

Possible future hardware options include:

- Lenovo ThinkCentre Tiny
- Dell OptiPlex Micro
- HP EliteDesk Mini
- Intel NUC
- Similar low-power mini-PC

A dedicated server would make it possible to keep the homelab running all the time without affecting the main computer.

## Version 1 Decision

For version 1, the project uses a virtual machine on my main Windows PC.

A dedicated physical server is not required for the first version because the current VM setup is enough to demonstrate the core goals of the project:

- Linux server administration
- SSH access
- Firewall configuration
- Security hardening
- Docker services
- Monitoring
- Technical documentation

This setup provides a complete foundation for Secure Homelab v1 while keeping the environment simple and easy to manage.
