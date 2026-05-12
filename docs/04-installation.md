# 04 - Installation

## Installation Overview

This document describes the installation process for the Ubuntu Server virtual machine used in the Secure Homelab project.

The goal of this step is to create a working Linux server environment that can later be secured, configured and used to run Docker services.

## Installation Method

The first version of the homelab will be installed as a virtual machine on my main Windows PC.

The virtual machine will run Ubuntu Server LTS.

## Software Needed

The following software is needed for the installation:

| Software | Purpose |
|---|---|
| VirtualBox or VMware Workstation Player | Run the virtual machine |
| Ubuntu Server LTS ISO | Server operating system |
| Windows Terminal / PowerShell | Manage the project and connect with SSH |
| Git | Version control and documentation |

## Planned Virtual Machine Settings

| Setting | Value |
|---|---|
| VM Name | secure-homelab |
| Operating System | Ubuntu Server LTS |
| RAM | 4-6 GB |
| CPU | 2 cores |
| Disk | 60-100 GB |
| Network Mode | NAT at first |
| Hostname | secure-homelab |

## Step 1 - Download Ubuntu Server

Ubuntu Server LTS will be downloaded from the official Ubuntu website.

The LTS version is used because it is stable and receives long-term security updates.

## Step 2 - Create the Virtual Machine

The virtual machine will be created in VirtualBox or VMware.

Planned settings:

- Name: `secure-homelab`
- Type: Linux
- Version: Ubuntu 64-bit
- RAM: 4-6 GB
- CPU: 2 cores
- Disk: 60-100 GB
- Network: NAT

## Step 3 - Install Ubuntu Server

During installation, the following choices will be made:

| Installation Setting | Planned Choice |
|---|---|
| Language | English |
| Keyboard layout | Swedish or English |
| Installation type | Ubuntu Server |
| Network | DHCP |
| Storage | Use entire virtual disk |
| Profile username | olle |
| Server name | secure-homelab |
| OpenSSH Server | Install |
| Featured server snaps | None for now |

## Step 4 - First Login

After installation, I will log in directly through the VM console using the user created during installation.

Planned username:

```text
olle
```

Planned hostname:

```text
secure-homelab
```

## Step 5 - Update the System

After the first login, the system should be updated.

Planned commands:

```bash
sudo apt update
sudo apt upgrade -y
```

## Step 6 - Install Basic Tools

The following basic tools will be installed:

```bash
sudo apt install git curl htop net-tools ufw -y
```

Purpose of the tools:

| Tool | Purpose |
|---|---|
| git | Version control |
| curl | Test connections and download resources |
| htop | Monitor CPU and RAM usage |
| net-tools | Network tools |
| ufw | Simple firewall management |

## Step 7 - Check IP Address

The server IP address will be checked with:

```bash
hostname -I
```

or:

```bash
ip a
```

The IP address will be documented here after installation:

```text
Server IP address: To be added after installation
```

## Step 8 - Test SSH Access

After OpenSSH is installed and the IP address is known, SSH access from the Windows host will be tested.

Planned command from Windows Terminal:

```bash
ssh olle@server-ip-address
```

Example format:

```bash
ssh olle@192.168.1.50
```

The exact command will be updated after installation.

## Step 9 - Document the Installation

After the installation is complete, this file will be updated with the actual configuration.

The following information should be documented:

- Virtualization software used
- Ubuntu Server version
- VM name
- RAM allocation
- CPU allocation
- Disk size
- Network mode
- Hostname
- Username
- IP address
- Any problems during installation
- How the problems were solved

## Installation Notes

This section will be updated during the actual installation.

Notes:

- To be added
- To be added
- To be added

## Problems and Solutions

Any problems during installation will be documented here.

| Problem | Cause | Solution |
|---|---|---|
| To be added | To be added | To be added |

## Installation Status

Status: Not installed yet

The next step is to install Ubuntu Server in the virtual machine and update this document with the actual installation details.
