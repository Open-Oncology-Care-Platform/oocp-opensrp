# DOCKER_SETUP

> **Project:** Open Oncology Care Platform (OOCP)
> **Repository:** `oocp-opensrp`
> **Version:** 1.0.0
> **Status:** Living Document
> **Last Updated:** July 2026

---

# Table of Contents

1. Purpose
2. Why Docker?
3. Deployment Philosophy
4. Docker Architecture
5. Prerequisites
6. Installing Docker
7. Installing Docker Compose
8. Verify Installation
9. Docker Concepts
10. OOCP Docker Directory Structure
11. Docker Networks
12. Docker Volumes
13. Docker Images
14. Container Naming Standards
15. Environment Variables
16. Useful Docker Commands
17. Docker Best Practices
18. Troubleshooting
19. References

---

# 1. Purpose

This document describes the Docker environment used by the Open Oncology Care Platform (OOCP).

It provides a standard approach for installing Docker, organising containers, managing networks and volumes, and running the OpenSRP ecosystem consistently across development environments.

---

# 2. Why Docker?

OOCP adopts Docker because it provides:

* Consistent development environments
* Reproducible deployments
* Simplified dependency management
* Service isolation
* Easy upgrades and rollbacks
* Portable deployments
* Foundation for future Kubernetes adoption

Every major OOCP component is expected to run in its own container.

---

# 3. Deployment Philosophy

The platform follows a **container-first** strategy.

Key principles include:

* One responsibility per container
* Stateless application containers
* Persistent data stored in Docker volumes
* Infrastructure defined as code
* Configuration externalised through environment variables
* Secure communication between services
* Reproducible deployments

---

# 4. Docker Architecture

The initial OOCP deployment consists of multiple cooperating containers.

```text id="2a6yrw"
                   Docker Engine
                         │
        ┌────────────────┼─────────────────┐
        │                │                 │
        ▼                ▼                 ▼
  OpenSRP Backend   PostgreSQL      Keycloak
        │                │                 │
        └────────────┬───┴─────────────────┘
                     ▼
               Docker Network
                     │
        ┌────────────┴─────────────┐
        ▼                          ▼
    HAPI FHIR                 OpenEMR
                     │
                     ▼
              SMART Applications
```

Each service communicates over an isolated Docker bridge network.

---

# 5. Prerequisites

Before using Docker, ensure:

* Ubuntu Linux is installed
* Git is installed
* Internet connectivity is available
* User belongs to the `docker` group
* Docker service is running
* Sufficient disk space is available

Refer to `SYSTEM_REQUIREMENTS.md` for detailed requirements.

---

# 6. Installing Docker

Ubuntu users can install Docker by following the official Docker installation guide.

After installation, verify that the Docker service is active.

```bash
sudo systemctl status docker
```

Enable Docker to start automatically:

```bash
sudo systemctl enable docker
```

---

# 7. Installing Docker Compose

Docker Compose v2 is included with modern Docker installations.

Verify installation:

```bash
docker compose version
```

Expected output:

```text
Docker Compose version v2.x.x
```

---

# 8. Verify Installation

Run the following commands:

```bash
docker --version

docker compose version

docker ps

docker info
```

These commands confirm:

* Docker Engine is installed
* Docker Compose is available
* Docker daemon is running
* Client can communicate with the daemon

---

# 9. Docker Concepts

## Docker Image

A read-only template used to create containers.

Examples:

* OpenSRP
* PostgreSQL
* Keycloak
* HAPI FHIR
* OpenEMR

---

## Docker Container

A running instance of an image.

Containers are:

* Isolated
* Lightweight
* Disposable
* Portable

---

## Docker Volume

A persistent storage location independent of the container lifecycle.

Used for:

* Databases
* Uploaded files
* Configuration
* Logs

---

## Docker Network

A virtual network allowing containers to communicate securely.

OOCP uses a dedicated bridge network for internal communication.

---

# 10. OOCP Docker Directory Structure

Recommended layout:

```text
~/OOCP/
│
├── deployments/
│   ├── docker-compose.yml
│   ├── .env
│   ├── opensrp/
│   ├── postgres/
│   ├── keycloak/
│   ├── hapi/
│   ├── openemr/
│   └── nginx/
│
├── repositories/
│
├── logs/
│
├── backups/
│
└── scripts/
```

This structure separates deployment assets from source code.

---

# 11. Docker Networks

A dedicated bridge network should connect all OOCP services.

Example services include:

* OpenSRP Backend
* PostgreSQL
* Keycloak
* HAPI FHIR
* OpenEMR

Benefits include:

* Internal service discovery
* Improved security
* Simplified communication
* Reduced host port exposure

---

# 12. Docker Volumes

Persistent Docker volumes should be created for:

| Service    | Volume Purpose                |
| ---------- | ----------------------------- |
| PostgreSQL | Database files                |
| Keycloak   | Identity data                 |
| HAPI FHIR  | FHIR persistence              |
| OpenEMR    | Application and database data |
| Logs       | Optional log storage          |

Volumes allow containers to be recreated without losing application data.

---

# 13. Docker Images

Core images planned for OOCP:

| Component        | Purpose                   |
| ---------------- | ------------------------- |
| PostgreSQL       | Database                  |
| Keycloak         | Identity Provider         |
| OpenSRP Backend  | Business services         |
| HAPI FHIR        | Interoperability          |
| OpenEMR          | Electronic Medical Record |
| Nginx *(future)* | Reverse proxy             |

Images should always be obtained from trusted or official sources where available.

---

# 14. Container Naming Standards

To improve consistency, container names should follow this convention:

```text
oocp-opensrp

oocp-postgres

oocp-keycloak

oocp-hapi

oocp-openemr

oocp-nginx
```

Networks:

```text
oocp-network
```

Volumes:

```text
oocp-postgres-data

oocp-keycloak-data

oocp-hapi-data

oocp-openemr-data
```

---

# 15. Environment Variables

Configuration should be managed through environment variables.

Typical values include:

* Database host
* Database port
* Database username
* Database password
* OAuth endpoints
* FHIR server URL
* Logging level
* Application ports

Sensitive information must be stored outside version control.

---

# 16. Useful Docker Commands

List running containers:

```bash
docker ps
```

List all containers:

```bash
docker ps -a
```

List Docker images:

```bash
docker images
```

List Docker volumes:

```bash
docker volume ls
```

List Docker networks:

```bash
docker network ls
```

View container logs:

```bash
docker logs <container-name>
```

Inspect a container:

```bash
docker inspect <container-name>
```

Stop a container:

```bash
docker stop <container-name>
```

Start a container:

```bash
docker start <container-name>
```

Remove a container:

```bash
docker rm <container-name>
```

Remove an image:

```bash
docker rmi <image-name>
```

---

# 17. Docker Best Practices

Contributors should:

* Use official images where possible.
* Pin image versions instead of using `latest`.
* Keep images updated.
* Store data in volumes.
* Use descriptive container names.
* Avoid running containers as root when possible.
* Keep secrets out of images and repositories.
* Minimise the number of exposed ports.
* Clean up unused images and containers regularly.

---

# 18. Troubleshooting

| Issue                       | Possible Cause                 | Suggested Action                                       |
| --------------------------- | ------------------------------ | ------------------------------------------------------ |
| Docker daemon unavailable   | Docker service stopped         | Start the Docker service                               |
| Port already in use         | Port conflict                  | Change the mapped port or stop the conflicting service |
| Container exits immediately | Configuration error            | Review container logs                                  |
| Cannot connect to database  | Database container unavailable | Check PostgreSQL container status                      |
| Network communication fails | Incorrect Docker network       | Inspect network configuration                          |

Useful diagnostic commands:

```bash
docker ps -a

docker logs <container-name>

docker network inspect <network-name>

docker volume ls
```

---

# 19. References

* Docker Documentation
* Docker Compose Documentation
* PostgreSQL Documentation
* Keycloak Documentation
* HAPI FHIR Documentation
* OpenSRP Documentation
* OpenEMR Documentation

---

# Revision History

| Version | Date      | Description                |
| ------- | --------- | -------------------------- |
| 1.0.0   | July 2026 | Initial Docker setup guide |

---

# Conclusion

Docker provides the foundation for the OOCP deployment strategy by enabling reproducible, isolated, and maintainable environments. Through standardised container naming, persistent storage, dedicated networking, and documented deployment practices, contributors can confidently deploy and manage the OpenSRP ecosystem while preparing the platform for future cloud-native and production-scale deployments.
