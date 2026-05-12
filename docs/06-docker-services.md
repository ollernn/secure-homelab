# 06 - Docker Services

## Docker Services Overview

This document describes the Docker-based services planned for the Secure Homelab project.

The goal is to use Docker and Docker Compose to run internal services for management, monitoring and navigation inside the homelab.

Version 1 focuses on a small number of useful services instead of a large and complex setup.

## Why Docker?

Docker is used because it makes it easier to run and manage services in isolated containers.

Using Docker also makes the environment easier to document, rebuild and expand later.

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

## Planned Services

| Service | Purpose | Status |
|---|---|---|
| Portainer | Manage Docker containers through a web interface | Planned |
| Uptime Kuma | Monitor service availability | Planned |
| Homepage | Dashboard for homelab services | Planned |
| Nginx | Web server / reverse proxy | Planned |

## Portainer

Portainer will be used to manage Docker containers, images, networks and volumes through a web interface.

Planned use:

- View running containers
- Manage Docker services
- Inspect logs
- Learn Docker management through a GUI

Expected port:

```text
9000
```

Status:

```text
Not installed yet
```

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

1. Docker
2. Docker Compose
3. Portainer
4. Uptime Kuma
5. Homepage
6. Nginx

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

| Port | Service | Access |
|---:|---|---|
| 9000 | Portainer | Internal only |
| 3001 | Uptime Kuma | Internal only |
| 80 | Nginx | Internal only |
| 443 | Nginx | Future/internal only |

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

Status: Planned

Docker and the planned services have not been installed yet.

This document will be updated after Docker, Docker Compose and the first services have been configured.
