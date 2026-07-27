# LOCAL_DEVELOPMENT

> **Project:** Open Oncology Care Platform (OOCP)
> **Repository:** `oocp-opensrp`
> **Version:** 1.0.0
> **Status:** Living Document
> **Last Updated:** July 2026

---

# Table of Contents

1. Purpose
2. Scope
3. Development Philosophy
4. Recommended Development Platform
5. Workstation Preparation
6. Directory Structure
7. Required Software
8. Development Workflow
9. Docker Development Environment
10. Git Workflow
11. Environment Variables
12. Development Best Practices
13. Troubleshooting
14. References

---

# 1. Purpose

This document describes how to prepare a local development environment for the Open Smart Register Platform (OpenSRP) within the Open Oncology Care Platform (OOCP).

The objective is to provide a consistent, reproducible, and secure development environment that enables contributors to build, test, and integrate OpenSRP and related healthcare interoperability services.

---

# 2. Scope

This guide applies to:

* Local development
* Feature development
* Bug fixes
* Integration testing
* Learning and experimentation
* Documentation updates

It is intended for developers, architects, contributors, and students working on OOCP.

---

# 3. Development Philosophy

OOCP adopts a **Documentation First** and **Infrastructure as Code** approach.

Every contributor is expected to:

* Understand the architecture before implementation.
* Maintain documentation alongside code.
* Follow established coding standards.
* Use containerised development environments.
* Keep local environments reproducible.
* Test changes before committing.

---

# 4. Recommended Development Platform

The recommended development platform is:

| Component        | Recommendation                   |
| ---------------- | -------------------------------- |
| Operating System | Ubuntu Linux (LTS)               |
| IDE              | Visual Studio Code               |
| Java             | OpenJDK 17 LTS                   |
| Docker           | Latest stable release            |
| Docker Compose   | Version 2 or later               |
| Git              | Latest stable version            |
| Browser          | Google Chrome or Mozilla Firefox |

Linux provides the closest match to typical production environments and is therefore the preferred platform.

---

# 5. Workstation Preparation

Before beginning development:

* Install the operating system.
* Update all system packages.
* Install Git.
* Install Docker Engine.
* Install Docker Compose.
* Install Java 17.
* Install Visual Studio Code.
* Verify internet connectivity.
* Configure SSH keys for GitHub (recommended).

Verify the installation using:

```bash
docker --version
docker compose version
java -version
git --version
```

---

# 6. Directory Structure

The recommended workspace structure is:

```text
~/OOCP/
│
├── repositories/
│   ├── opensrp/
│   ├── hapi/
│   ├── openemr/
│   ├── oncology-ig/
│   └── smart-apps/
│
├── deployments/
│
├── downloads/
│
├── backups/
│
├── logs/
│
└── scripts/
```

### Directory Descriptions

| Directory    | Purpose                                    |
| ------------ | ------------------------------------------ |
| repositories | Source code repositories                   |
| deployments  | Docker Compose files and deployment assets |
| downloads    | Installation packages and archives         |
| backups      | Database and configuration backups         |
| logs         | Local application and container logs       |
| scripts      | Utility and automation scripts             |

Keeping a consistent directory structure simplifies maintenance and troubleshooting.

---

# 7. Required Software

The following software should be installed before development begins.

## Core Tools

* Git
* Docker Engine
* Docker Compose
* Java Development Kit (JDK 17)

## Recommended Tools

* Visual Studio Code
* pgAdmin
* Portainer
* Adminer
* Postman or Bruno
* Draw.io Desktop

## Optional Tools

* IntelliJ IDEA Community Edition
* DBeaver
* Maven
* OpenSSL
* GitHub CLI

---

# 8. Development Workflow

The standard OOCP workflow is:

```text
Pull Latest Changes
        │
        ▼
Review Documentation
        │
        ▼
Create Feature Branch
        │
        ▼
Implement Changes
        │
        ▼
Run Local Tests
        │
        ▼
Update Documentation
        │
        ▼
Commit Changes
        │
        ▼
Push Branch
        │
        ▼
Create Pull Request
```

Documentation updates should accompany code changes whenever applicable.

---

# 9. Docker Development Environment

All core services are expected to run within Docker containers.

Initial services include:

* OpenSRP Backend
* PostgreSQL
* Keycloak
* HAPI FHIR
* OpenEMR

Docker Compose will be used to orchestrate these services during local development.

Persistent Docker volumes should be used to preserve application data between container restarts.

---

# 10. Git Workflow

Contributors should follow a feature-branch workflow.

Typical process:

1. Pull the latest changes from the default branch.
2. Create a descriptive feature branch.
3. Make changes.
4. Test locally.
5. Update relevant documentation.
6. Commit using meaningful commit messages.
7. Push the branch.
8. Open a Pull Request for review.

Commit messages should clearly describe the purpose of each change.

Examples:

```text
Add OpenSRP deployment documentation

Implement patient registration endpoint

Fix Docker networking configuration

Update FHIR architecture documentation
```

---

# 11. Environment Variables

Configuration values should never be hard-coded.

Environment-specific settings should be stored in environment variable files (for example, `.env`) and excluded from version control when they contain sensitive information.

Typical configuration includes:

* Database connection settings
* Authentication server URLs
* FHIR server endpoints
* API ports
* Logging levels
* Feature flags

Secrets such as passwords, client secrets, and API keys must never be committed to Git repositories.

---

# 12. Development Best Practices

All contributors are encouraged to:

* Read the relevant architecture documentation before coding.
* Write small, focused commits.
* Keep Docker containers up to date.
* Follow the project's coding standards.
* Maintain backwards compatibility where practical.
* Document architectural decisions.
* Test all changes locally before pushing.

Development should prioritise code quality, readability, and maintainability over rapid implementation.

---

# 13. Troubleshooting

Common issues may include:

| Issue                           | Possible Cause                  | Suggested Action                                   |
| ------------------------------- | ------------------------------- | -------------------------------------------------- |
| Docker container fails to start | Port conflict                   | Check running containers and port assignments      |
| Unable to connect to database   | Database not running            | Verify PostgreSQL container status                 |
| Git authentication issues       | Missing SSH key                 | Configure GitHub SSH authentication                |
| Java not found                  | JAVA_HOME not configured        | Verify Java installation and environment variables |
| Container networking issues     | Docker network misconfiguration | Inspect Docker networks and service names          |

Refer to `TROUBLESHOOTING.md` for detailed guidance.

---

# 14. References

Related documentation:

* `deployment/README.md`
* `SYSTEM_REQUIREMENTS.md`
* `INSTALLATION_GUIDE.md`
* `DOCKER_SETUP.md`
* `architecture/DEPLOYMENT_ARCHITECTURE.md`
* `architecture/SYSTEM_ARCHITECTURE.md`
* `architecture/FHIR_ARCHITECTURE.md`
* `oocp-governance/CODE_STYLE.md`
* `oocp-governance/CONTRIBUTING.md`

---

# Revision History

| Version | Date      | Description                                 |
| ------- | --------- | ------------------------------------------- |
| 1.0.0   | July 2026 | Initial local development environment guide |

---

# Conclusion

A consistent local development environment is essential for building reliable healthcare software. By standardising workstation preparation, tooling, workflows, and development practices, the Open Oncology Care Platform ensures that contributors can focus on delivering high-quality, interoperable healthcare solutions while minimising environment-specific issues and improving collaboration across the project.
