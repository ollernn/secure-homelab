# 02 - Hardware and Virtual Machine

## Host Machine

The first version of the homelab is built on my main Windows PC.

This means that the server environment will run inside a virtual machine instead of on separate physical hardware.

## Host Specifications

| Component | Specification |
|---|---|
| CPU | AMD Ryzen 5 5600X / 6-Core Processor |
| RAM | 32 GB |
| GPU | NVIDIA GeForce RTX 3060 Ti, 8 GB |
| Storage | 2.27 TB |
| Operating System | Windows |

## Why I Am Using a Virtual Machine

The first version of this project will be built in a virtual machine.

This is a good starting point because it allows me to build and test a server environment without buying separate hardware at the beginning of the project.

A virtual machine also makes the lab easier to manage. It can be started when I want to work on the project and shut down when I want to use my main computer normally.

## Benefits of Using a Virtual Machine

Using a virtual machine has several advantages:

- No extra hardware is required
- The lab can be started and stopped when needed
- The host computer is only affected while the VM is running
- The environment is easy to rebuild if something goes wrong
- It is a safe way to learn Linux server administration
- It makes the first version of the project cheaper and easier to start

## Planned Virtual Machine Resources

The virtual machine will be given enough resources to run Ubuntu Server, Docker and a few internal services.

| Resource | Planned Allocation |
|---|---:|
| RAM | 4-6 GB |
| CPU | 2 cores |
| Disk | 60-100 GB |
| Operating System | Ubuntu Server 26.04 LTS |
| Network Mode | NAT at first, Bridged later if needed |

## Why These Resources Are Enough

The first version of the homelab will only run a small number of services.

The planned services are:

- Portainer
- Uptime Kuma
- Homepage
- Nginx

These services do not require a powerful server. The planned VM resources are enough for learning, testing and documentation.

Because the host computer has 32 GB of RAM and a 6-core processor, it can run the VM while still having enough resources left for normal use.

## Performance Impact

The host computer will mainly be affected when the virtual machine is running.

When the VM is turned off, it will not use CPU or RAM. It will only take up disk space.

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

For version 1, the project will use a virtual machine on my main Windows PC.

A dedicated physical server is not required for the first version.
