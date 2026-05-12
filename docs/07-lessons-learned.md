# 07 - Lessons Learned

## Purpose of This Document

This document is used to track what I learn during the Secure Homelab project.

The goal is to document not only the final result, but also the learning process, problems, decisions and improvements made during the project.

## Learning Goals

The main learning goals for version 1 are:

- Understand how to set up a Linux server in a virtual machine
- Learn basic Linux server administration
- Configure SSH access
- Apply basic server security
- Use a firewall to control network access
- Install and manage Docker
- Run internal services with Docker Compose
- Monitor services
- Document a technical infrastructure project
- Create a portfolio-ready project

## Learning Log

### Session 1 - Project Planning and Documentation

**Date:** 2026-05-12

**What I did:**

- Created the project repository
- Created the initial folder structure
- Wrote the first README file
- Added documentation files for overview, hardware, network, installation, security and Docker services

**What I learned:**

- A technical project becomes easier to manage when it has a clear structure from the beginning
- GitHub can be used not only for code, but also for technical documentation
- Planning the scope of version 1 helps prevent the project from becoming too large too early

**Problems:**

- Some markdown code blocks were not copied completely at first

**Solution:**

- Replaced incomplete files with complete markdown versions
- Checked each documentation file before continuing

**Next step:**

- Install Ubuntu Server in a virtual machine


---

### Session 2 - Ubuntu Server Installation

**Date:** 2026-05-12

**What I did:**

- Installed Oracle VirtualBox on the Windows host machine
- Downloaded Ubuntu Server 26.04 LTS
- Created a virtual machine named `secure-homelab`
- Allocated 4096 MB RAM, 2 CPU cores and an 80 GB virtual disk
- Installed Ubuntu Server manually
- Selected English as the installation language
- Used a Swedish keyboard layout
- Installed OpenSSH Server during installation
- Skipped Ubuntu Pro
- Did not install any featured server snaps
- Booted successfully into the installed server
- Logged in with the created user account
- Checked the Ubuntu version, hostname and network interface
- Updated the system
- Installed basic tools: `git`, `curl`, `htop`, `net-tools` and `ufw`

**What I learned:**

- A virtual machine can be used as a safe server environment without affecting the main computer when it is turned off
- NAT networking gives the VM internet access through the host computer
- Ubuntu Server does not use a graphical desktop by default
- The command `ip a` is useful for finding the real network interface and IP address
- `hostname -i` can show a local hostname address and should not always be used as the SSH address
- OpenSSH can be installed directly during the Ubuntu Server installation

**Problems:**

- VirtualBox showed the guest OS type as Ubuntu 25.04 even though the ISO file was Ubuntu Server 26.04 LTS
- I accidentally entered the GRUB edit screen during boot
- `hostname -i` showed `127.0.1.1`, which was not the correct address for SSH access

**Solutions:**

- Continued with the installation because the selected ISO file was correct
- Exited the GRUB edit screen and started the normal Ubuntu Server installation
- Used `ip a` to find the correct IPv4 address under the `enp0s3` interface

**Next step:**

- Test SSH access from Windows Terminal
- Begin basic security configuration


---

### Session 3 - SSH Access and Port Forwarding

**Date:** 2026-05-12

**What I did:**

- Tested SSH access from Windows Terminal / PowerShell
- First tried to connect directly to the VM NAT IP address with `ssh olle@10.0.2.15`
- Found that the connection timed out
- Checked that the SSH service was running on the Ubuntu server
- Verified that SSH was active with `sudo systemctl status ssh`
- Configured VirtualBox port forwarding for SSH
- Connected successfully using `ssh -p 2222 olle@127.0.0.1`

**What I learned:**

- VirtualBox NAT allows the VM to access the internet, but does not automatically expose services back to the host
- SSH can be active inside the VM even if the host cannot connect directly to the VM IP address
- Port forwarding can map a port on the Windows host to a port inside the VM
- `127.0.0.1:2222` on the host can be forwarded to port `22` inside the Ubuntu server
- `systemctl status ssh` is useful for checking whether the SSH service is running

**Problems:**

- SSH to `10.0.2.15` timed out
- SSH to `127.0.0.1:2222` was refused before the port forwarding rule was corrected
- I accidentally typed `systemct1` instead of `systemctl`

**Solutions:**

- Confirmed that SSH was active on the Ubuntu server
- Corrected the `systemctl` command
- Added a VirtualBox port forwarding rule from host port `2222` to guest port `22`
- Connected successfully with `ssh -p 2222 olle@127.0.0.1`

**Next step:**

- Configure SSH keys
- Harden SSH settings
- Enable and configure the UFW firewall
---

## Problems and Solutions

| Problem | Cause | Solution |
|---|---|---|
| Incomplete markdown files | Some code blocks were not copied fully | Replaced the files with complete versions |

## Technical Concepts Learned

This section will be updated throughout the project.

Planned concepts:

- Virtual machines
- NAT networking
- Bridged networking
- SSH
- Linux users and permissions
- UFW firewall
- fail2ban
- Docker
- Docker Compose
- Service monitoring
- Technical documentation

## Decisions Made

| Decision | Reason |
|---|---|
| Use a virtual machine for version 1 | Avoid buying hardware before the basic lab is working |
| Use Ubuntu Server 26.04 LTS | Stable, current, common and well documented |
| Start with NAT networking | Simple and safer starting point |
| Keep services internal only | Reduces risk while learning |
| Use GitHub for detailed documentation | Makes the project easier to review technically |
| Use the portfolio website for a summary | Makes the project easier to understand quickly |

## Reflection

This project starts with documentation and planning before the practical installation.

The purpose is not to make the project look finished before it is built, but to create a clear structure that can be updated as the lab develops.

As the project continues, this document will be updated with real problems, commands, decisions and lessons learned.

## Next Learning Areas

The next areas to learn are:

- Connecting to the server with SSH from Windows Terminal
- Creating and using SSH keys
- Understanding basic Linux users and permissions
- Configuring UFW firewall rules
- Installing and configuring fail2ban
- Securing the server before installing Docker services

## Current Status

Status: Ubuntu Server installed

Ubuntu Server 26.04 LTS is installed and running in a VirtualBox virtual machine.

The next step is to test SSH access from Windows Terminal and begin the basic security configuration.
