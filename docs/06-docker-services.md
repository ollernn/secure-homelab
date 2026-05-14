# 06 - Docker Services

## Docker Services Overview

This document describes the Docker-based services used and planned for the Secure Homelab project.

The goal is to use Docker and Docker Compose to run internal services for management, monitoring and navigation inside the homelab.

Version 1 focuses on a small number of useful services instead of a large and complex setup.

## Why Docker?

Docker is used because it makes it easier to run and manage services in isolated containers.

Using Docker also makes the environment easier to document, rebuild and expand later.

## Docker Installation

Docker and Docker Compose were installed on the Ubuntu Server VM using apt.

Installation command:

```bash
sudo apt update
sudo apt install docker.io docker-compose-v2 -y
```

Docker was enabled and started with:

```bash
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker
```

The Docker service was verified as active:

```text
Active: active (running)
```

## Docker User Group

The user `olle` was added to the Docker group to allow Docker commands without using `sudo`.

Command used:

```bash
sudo usermod -aG docker $USER
```

After this, the SSH session was closed and reopened so that the new group membership would apply.

## Installed Versions

Docker version was checked with:

```bash
docker --version
```

Result:

```text
Docker version 29.1.3
```

Docker Compose version was checked with:

```bash
docker compose version
```

Result:

```text
Docker Compose version 2.40.3
```

## Docker Test

Docker was tested with the official `hello-world` container.

Command used:

```bash
docker run hello-world
```

Result:

```text
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

The container list was checked with:

```bash
docker ps -a
```

The `hello-world` test container was visible with status `Exited`.

## Planned Docker Setup

The first version will use:

- Docker
- Docker Compose
- Separate folders for each service
- Internal-only access
- Documentation for each service

Planned folder structure:

```text
docker/
├── portainer/
├── uptime-kuma/
├── homepage/
└── nginx/
```

## Docker Services

| Service | Purpose | Status |
|---|---|---|
| Portainer | Manage Docker containers through a web interface | Installed |
| Uptime Kuma | Monitor service availability | Planned |
| Homepage | Dashboard for homelab services | Planned |
| Nginx | Web server / reverse proxy | Planned |

## Portainer

Portainer is used to manage Docker containers, images, networks and volumes through a web interface.

It was installed as the first internal Docker service in the homelab.

### Purpose

Portainer is included to:

- View running containers
- Manage Docker services
- Inspect logs
- Learn Docker management through a GUI
- Make the homelab easier to manage visually

### Docker Volume

A Docker volume was created to store Portainer data:

```bash
docker volume create portainer_data
```

The volume was verified with:

```bash
docker volume ls
```

### Installation Command

Portainer was started with:

```bash
docker run -d \
  -p 9443:9443 \
  --name portainer \
  --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce:sts
```

### Container Status

The container was checked with:

```bash
docker ps
```

Result:

```text
portainer/portainer-ce:sts   Up   0.0.0.0:9443->9443/tcp
```

### Logs

Portainer logs were checked with:

```bash
docker logs portainer
```

The logs showed that Portainer started successfully and generated self-signed SSL certificates.

### Access

Portainer is accessed from the Windows host through VirtualBox port forwarding:

```text
https://127.0.0.1:9443
```

An admin account was created through the web interface.

The password is not documented in this repository.

### Status

Status: Installed and working

## Uptime Kuma

Uptime Kuma will be used to monitor whether internal services are online.

Planned use:

- Monitor Portainer
- Monitor Homepage
- Monitor Nginx
- Learn basic service monitoring

Expected port:

```text
3001
```

Status:

```text
Not installed yet
```

## Homepage

Homepage will be used as a simple dashboard for the homelab.

Planned use:

- Show links to internal services
- Organize the homelab visually
- Create a clearer overview of the environment

Status:

```text
Not installed yet
```

## Nginx

Nginx will be used as a web server and may later be used as a reverse proxy.

Planned use:

- Serve a simple test page
- Learn basic web server configuration
- Prepare for future reverse proxy setup

Expected ports:

```text
80
443
```

Status:

```text
Not installed yet
```

## Docker Compose

Docker Compose will be used to define and run the services.

Each service will have its own folder and compose file when needed.

Example structure:

```text
docker/
└── uptime-kuma/
    └── docker-compose.yml
```

## Planned Installation Order

The services will be installed in this order:

1. Portainer
2. Uptime Kuma
3. Homepage
4. Nginx

Docker and Docker Compose are already installed and verified.

## Security Considerations

The Docker services in version 1 will only be used internally.

Management interfaces such as Portainer should not be exposed to the public internet.

Important security considerations:

- Keep services internal only
- Avoid exposing unnecessary ports
- Document every exposed port
- Use firewall rules to limit access
- Avoid storing secrets directly in public files
- Keep containers updated

## Planned Ports

| Port | Service | Access | Status |
|---:|---|---|---|
| 9000 | Portainer | Internal only | Not opened yet |
| 3001 | Uptime Kuma | Internal only | Not opened yet |
| 80 | Nginx | Internal only | Not opened yet |
| 443 | Nginx | Future/internal only | Not opened yet |

The final port list will be updated after implementation.

## Documentation Plan

For each Docker service, the following should be documented:

- What the service does
- Why it is included
- How it was installed
- Which port it uses
- How it is accessed
- Any problems during setup
- Screenshots when relevant

## Docker Services Status

Status: Docker installed and verified

Docker and Docker Compose are installed and working.

The next step is to deploy the first internal service, Portainer.
