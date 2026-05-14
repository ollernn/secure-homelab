# 04 - Installation

## Installation Overview

This document describes the installation process for the Ubuntu Server virtual machine used in the Secure Homelab project.

The goal of this step was to create the base Linux server environment used for the rest of Secure Homelab v1.

## Installation Method

The first version of the homelab was installed as a virtual machine on my main Windows PC.

The virtual machine runs Ubuntu Server 26.04 LTS.

## Software and Tools Used

| Software | Purpose |
|---|---|
| Oracle VirtualBox 7.2.8 | Run the virtual machine |
| Ubuntu Server 26.04 LTS ISO | Server operating system |
| Windows Terminal / PowerShell | Manage the project and connect with SSH |
| Git | Version control and documentation |

## Virtual Machine Settings

| Setting | Value |
|---|---|
| VM Name | secure-homelab |
| Operating System | Ubuntu Server 26.04 LTS |
| RAM | 4096 MB |
| CPU | 2 cores |
| Disk | 80 GB |
| Network Mode | NAT |
| Hostname | secure-homelab |
| Local user | olle |

## Installation Choices

During installation, the following choices were made:

| Installation Setting | Choice |
|---|---|
| Language | English |
| Keyboard layout | Swedish |
| Installation type | Ubuntu Server |
| Third-party drivers | Not installed |
| Network | DHCP through NAT |
| Proxy | None |
| Ubuntu archive mirror | Default Ubuntu archive mirror |
| Storage | Use entire virtual disk |
| LVM | Not used |
| Disk encryption | Not used |
| Ubuntu Pro | Skipped |
| OpenSSH Server | Installed |
| Password authentication over SSH | Enabled during installation, disabled later during SSH hardening |
| Featured server snaps | None selected |

## Storage Configuration

The server was installed on the VirtualBox virtual disk.

| Disk | Size | File system | Mount point |
|---|---:|---|---|
| VBOX_HARDDISK | 80 GB | ext4 | `/` |

The virtual disk is stored on the host computer under the VirtualBox VM folder.

## First Login

After installation and reboot, I logged in successfully using the created user account.

| Field | Value |
|---|---|
| Local user | olle |
| Hostname | secure-homelab |

## System Information

The following command was used to check the Ubuntu version:

```bash
lsb_release -a
```

Result:

```text
Distributor ID: Ubuntu
Description:    Ubuntu 26.04 LTS
Release:        26.04
Codename:       resolute
```

The hostname was checked with:

```bash
hostname
```

Result:

```text
secure-homelab
```

## Network Information

The network interface was checked with:

```bash
ip a
```

Result:

| Field | Value |
|---|---|
| Interface | enp0s3 |
| IPv4 address | 10.0.2.15 |
| Network mode | NAT |

The command `hostname -i` returned:

```text
127.0.1.1
```

This is not the address used for SSH access. The correct IPv4 address for the VM is shown under the `enp0s3` interface:

```text
10.0.2.15
```

## System Update

After the first login, the system was updated with:

```bash
sudo apt update
sudo apt upgrade -y
```

## Basic Tools Installed

The following basic tools were installed:

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

## Installation Notes

- Ubuntu Server 26.04 LTS was installed successfully.
- The VM was created in VirtualBox with 4096 MB RAM, 2 CPU cores and an 80 GB virtual disk.
- NAT networking was used for the first version.
- OpenSSH Server was installed during the Ubuntu installation.
- No featured server snaps were selected.
- Ubuntu Pro was skipped.
- The ISO file was removed from the virtual optical drive after installation.
- The server booted successfully from the virtual hard disk after reboot.
- SSH was tested from the Windows host after installation.
- Direct SSH access to `10.0.2.15` timed out because the VM was running behind VirtualBox NAT.
- A VirtualBox port forwarding rule was added from host port `2222` to guest port `22`.
- SSH access then worked using `ssh -p 2222 olle@127.0.0.1`.
- SSH password authentication was later disabled during the security hardening phase.
- SSH key authentication is now used for remote access.

## Problems and Solutions

| Problem | Cause | Solution |
|---|---|---|
| VirtualBox showed Ubuntu 25.04 as the guest OS type | VirtualBox did not correctly identify Ubuntu 26.04 yet | Continued with Ubuntu 64-bit because the ISO file was Ubuntu Server 26.04 LTS |
| Entered GRUB edit mode by mistake | Wrong key pressed during boot menu | Exited the edit screen and continued with the normal Ubuntu Server installation option |
| `hostname -i` showed `127.0.1.1` | This command returned a local hostname address | Used `ip a` to find the real VM IPv4 address on `enp0s3` |
| SSH to `10.0.2.15` timed out | VirtualBox NAT does not expose the guest SSH port directly to the host | Added a port forwarding rule from `127.0.0.1:2222` to guest port `22` |

## Installation Status

Status: Complete

Ubuntu Server 26.04 LTS is installed and running in a VirtualBox virtual machine.

The base installation was completed successfully and later secured, updated and extended with Docker services as part of Secure Homelab v1.
