# 06 - Docker Services

## Docker Services Overview

This document describes the Docker-based services deployed in Secure Homelab v1.

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

## Docker Setup

Version 1 uses:

- Docker
- Docker Compose
- Separate folders for service configuration
- Internal-only access through VirtualBox port forwarding
- Documentation for each service
- Docker volumes for persistent data
- A shared Docker network for internal service communication

Service folder structure:

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
| Uptime Kuma | Monitor service availability | Installed |
| Homepage | Dashboard for homelab services | Installed |
| Nginx | Test web server | Installed |

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

Uptime Kuma is used to monitor whether internal services are online.

It was installed as the second internal Docker service in the homelab.

### Purpose

Uptime Kuma is included to:

- Monitor internal services
- Track whether services are up or down
- Learn basic service monitoring
- Provide visibility into the homelab environment

### Docker Volume

A Docker volume was created to store Uptime Kuma data:

```bash
docker volume create uptime_kuma_data
```

The volume was verified with:

```bash
docker volume ls
```

### Installation Command

Uptime Kuma was started with:

```bash
docker run -d \
  --name uptime-kuma \
  --restart=always \
  -p 3001:3001 \
  -v uptime_kuma_data:/app/data \
  louislam/uptime-kuma:1
```

### Container Status

The container was checked with:

```bash
docker ps
```

Uptime Kuma was running and exposed on port `3001`.

### Access

Uptime Kuma is accessed from the Windows host through VirtualBox port forwarding:

```text
http://127.0.0.1:3001
```

An admin account was created through the web interface.

The password is not documented in this repository.

### Docker Network

A shared Docker network was created so that Uptime Kuma can monitor other containers by container name.

Command used:

```bash
docker network create homelab
```

Portainer and Uptime Kuma were connected to the network:

```bash
docker network connect homelab portainer
docker network connect homelab uptime-kuma
```

The network was checked with:

```bash
docker network inspect homelab
```

### Monitoring Portainer

The first monitor added in Uptime Kuma was Portainer.

The first attempt used:

```text
https://127.0.0.1:9443
```

This failed because `127.0.0.1` inside the Uptime Kuma container refers to the Uptime Kuma container itself.

The monitor was changed to use the Docker container name:

```text
https://portainer:9443
```

Because Portainer uses a self-signed certificate in this internal lab environment, TLS/SSL errors were ignored for this monitor.

Final result:

```text
Portainer: Up
Status code: 200 OK
```

### Status

Status: Installed and working

## Homepage

Homepage is used as an internal dashboard for the homelab.

It was installed as the third internal Docker service.

### Purpose

Homepage is included to:

- Provide a central dashboard for homelab services
- Link to Portainer and Uptime Kuma
- Make the homelab easier to navigate
- Create a clearer overview of the environment

### Folder Structure

Homepage was configured using files stored on the Ubuntu server:

```text
~/homelab/homepage/
├── docker-compose.yml
└── config/
    ├── services.yaml
    ├── settings.yaml
    ├── bookmarks.yaml
    ├── widgets.yaml
    └── docker.yaml
```

### Docker Compose

Homepage was deployed using Docker Compose.

The compose file was created at:

```text
~/homelab/homepage/docker-compose.yml
```

Docker Compose was used to start the service:

```bash
docker compose up -d
```

### Configuration

The main service links were configured in:

```text
services.yaml
```

Services added to the dashboard:

- Portainer
- Uptime Kuma
- Nginx

Basic dashboard settings were configured in:

```text
settings.yaml
```

### Access

Homepage is accessed from the Windows host through VirtualBox port forwarding:

```text
http://127.0.0.1:3000
```

### Monitoring

Homepage was added as a monitor in Uptime Kuma.

Uptime Kuma monitors Homepage internally through the Docker network:

```text
http://homepage:3000
```

Final result:

```text
Homepage: Up
Status code: 200 OK
```

### Status

Status: Installed and working

## Nginx

Nginx is used as a basic web server in the homelab.

It was installed as the fourth internal Docker service.

### Purpose

Nginx is included to:

- Serve a simple test web page
- Learn basic web server deployment with Docker
- Prepare for future reverse proxy configuration
- Provide a service that can be monitored by Uptime Kuma
- Provide a linkable service in the Homepage dashboard

### Folder Structure

Nginx was configured using files stored on the Ubuntu server:

```text
~/homelab/nginx/
├── docker-compose.yml
└── html/
    └── index.html
```

### Test Web Page

A simple HTML page was created at:

```text
~/homelab/nginx/html/index.html
```

The page contains a basic Secure Homelab test message.

### Docker Compose

Nginx was deployed using Docker Compose.

The compose file was created at:

```text
~/homelab/nginx/docker-compose.yml
```

Docker Compose was used to start the service:

```bash
docker compose up -d
```

### Access

Nginx is exposed on host port `8080`, which maps to container port `80`.

Access URL from the Windows host:

```text
http://127.0.0.1:8080
```

### Monitoring

Nginx was added as a monitor in Uptime Kuma.

Uptime Kuma monitors Nginx internally through the Docker network:

```text
http://nginx:80
```

Final result:

```text
Nginx: Up
Status code: 200 OK
```

### Homepage Dashboard

Nginx was added to the Homepage dashboard as a link.

Dashboard URL:

```text
http://127.0.0.1:3000
```

### Status

Status: Installed and working

## Docker Compose

Docker Compose is used to define and run services with YAML configuration files.

In version 1, Docker Compose was used for Homepage and Nginx.

Example structure:

```text
~/homelab/nginx/
├── docker-compose.yml
└── html/
    └── index.html
```

## Installation Order

The services were installed in this order:

1. Portainer
2. Uptime Kuma
3. Homepage
4. Nginx

This order made it possible to first manage Docker with Portainer, then add monitoring with Uptime Kuma, then create a dashboard with Homepage and finally add a test web server with Nginx.

## Security Considerations

The Docker services in version 1 are used internally.

Management interfaces such as Portainer should not be exposed to the public internet.

Important security considerations:

- Keep services internal only
- Avoid exposing unnecessary ports
- Document every exposed port
- Use firewall rules to limit access
- Avoid storing secrets directly in public files
- Keep containers updated

## Service Ports

| Host Port | Container Port | Service | Access | Status |
|---:|---:|---|---|---|
| 9443 | 9443 | Portainer | Internal only through port forwarding | Opened in UFW |
| 3001 | 3001 | Uptime Kuma | Internal only through port forwarding | Opened in UFW |
| 3000 | 3000 | Homepage | Internal only through port forwarding | Opened in UFW |
| 8080 | 80 | Nginx | Internal only through port forwarding | Opened in UFW |

## Documentation Plan

For each Docker service, the following is documented:

- What the service does
- Why it is included
- How it was installed
- Which port it uses
- How it is accessed
- Any problems during setup
- Screenshots when relevant

## Docker Services Status

Status: Complete for version 1

Docker and Docker Compose are installed and working.

The following internal Docker services are deployed and verified:

- Portainer
- Uptime Kuma
- Homepage
- Nginx

Portainer, Homepage and Nginx are monitored in Uptime Kuma.

Homepage provides dashboard links to Portainer, Uptime Kuma and Nginx.

## Docker Network Summary

A custom Docker network named `homelab` is used for internal container communication.

Connected containers:

- `portainer`
- `uptime-kuma`
- `homepage`
- `nginx`

This allows Uptime Kuma to monitor services internally using container names instead of host addresses.
