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
| Use Ubuntu Server LTS | Stable, common and well documented |
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

- Installing Ubuntu Server
- Connecting to the server with SSH
- Basic Linux commands
- Updating and managing packages
- Securing the server before installing services

## Current Status

Status: Planning completed

The next step is to install Ubuntu Server in a virtual machine and begin the practical setup.
