# Deployment Guide

> **Project:** Open Oncology Care Platform (OOCP)
> **Repository:** `oocp-opensrp`
> **Version:** 1.0.0
> **Status:** Living Document

---

# Overview

This directory contains all documentation related to deploying the **Open Smart Register Platform (OpenSRP)** as part of the **Open Oncology Care Platform (OOCP)**.

The deployment documentation is designed to provide a repeatable, secure, and standards-based process for setting up OpenSRP in local development, testing, and future production environments.

Rather than focusing only on installation commands, this documentation explains the reasoning behind the deployment architecture, infrastructure decisions, networking, security, and operational procedures.

---

# Deployment Philosophy

The OOCP project follows a **Documentation First** engineering approach.

Before deploying any infrastructure, contributors should understand:

* What components are being deployed
* Why each component exists
* How services communicate
* How healthcare data flows through the platform
* How security is implemented
* How interoperability is achieved

Deployment is therefore viewed as an engineering process rather than a collection of installation commands.

---

# Deployment Objectives

The deployment process aims to:

* Create a reproducible development environment
* Support container-based deployment using Docker
* Maintain consistent environments across developers
* Preserve application data using persistent storage
* Support healthcare interoperability standards
* Simplify future cloud deployment
* Encourage Infrastructure as Code (IaC)
* Promote secure deployment practices

---

# Deployment Environments

The project currently focuses on the following environments.

| Environment           | Purpose                            |
| --------------------- | ---------------------------------- |
| Local Development     | Individual developer workstations  |
| Testing               | Functional and integration testing |
| Staging *(Future)*    | Pre-production validation          |
| Production *(Future)* | Live healthcare deployment         |

---

# Deployment Documentation

The deployment directory contains the following documents.

| Document                      | Description                                 |
| ----------------------------- | ------------------------------------------- |
| **README.md**                 | Deployment documentation overview           |
| **DEPLOYMENT_PLAN.md**        | Overall deployment strategy and roadmap     |
| **SYSTEM_REQUIREMENTS.md**    | Hardware and software prerequisites         |
| **LOCAL_DEVELOPMENT.md**      | Preparing a development workstation         |
| **INSTALLATION_GUIDE.md**     | Step-by-step installation process           |
| **DOCKER_SETUP.md**           | Docker and Docker Compose configuration     |
| **NETWORK_CONFIGURATION.md**  | Docker networking and service communication |
| **DATABASE_CONFIGURATION.md** | PostgreSQL deployment and configuration     |
| **KEYCLOAK_CONFIGURATION.md** | Identity and authentication setup           |
| **HAPI_CONFIGURATION.md**     | HAPI FHIR integration                       |
| **OPENEMR_INTEGRATION.md**    | OpenEMR connectivity and interoperability   |
| **BACKUP_AND_RESTORE.md**     | Backup and disaster recovery procedures     |
| **TROUBLESHOOTING.md**        | Common deployment issues and solutions      |
| **RELEASE_PROCESS.md**        | Versioning and deployment lifecycle         |

Additional deployment documents may be introduced as the platform evolves.

---

# Deployment Workflow

The recommended deployment workflow is illustrated below.

```text
Prepare Development Environment
                │
                ▼
Verify System Requirements
                │
                ▼
Install Docker & Dependencies
                │
                ▼
Configure Infrastructure
                │
                ▼
Deploy Core Services
                │
                ▼
Verify Container Health
                │
                ▼
Configure Authentication
                │
                ▼
Configure FHIR Services
                │
                ▼
Integration Testing
                │
                ▼
Application Development
```

---

# Core Infrastructure

The initial OpenSRP deployment will consist of several cooperating services.

| Component       | Purpose                          |
| --------------- | -------------------------------- |
| OpenSRP Backend | Business logic and REST APIs     |
| PostgreSQL      | Primary relational database      |
| Keycloak        | Identity and Access Management   |
| HAPI FHIR       | HL7 FHIR interoperability server |
| OpenEMR         | Electronic Medical Record        |
| Docker          | Container runtime                |
| Docker Compose  | Multi-container orchestration    |

Future releases may include additional infrastructure such as monitoring, logging, reverse proxies, and Kubernetes orchestration.

---

# Deployment Principles

The OOCP deployment architecture follows these engineering principles.

* Documentation First
* Infrastructure as Code (IaC)
* Container-First Deployment
* Security by Design
* Least Privilege
* Reproducibility
* Standards-Based Interoperability
* Automation
* Continuous Improvement

---

# Prerequisites

Before beginning deployment, ensure the development workstation meets the documented requirements.

Typical prerequisites include:

* Ubuntu Linux (recommended)
* Git
* Docker Engine
* Docker Compose
* Java Development Kit (JDK)
* Stable internet connection
* Sufficient CPU, memory, and storage resources

Refer to **SYSTEM_REQUIREMENTS.md** for detailed specifications.

---

# Related Documentation

This deployment guide should be read alongside the following project documents:

* `README.md`
* `Glossary.md`
* `research/opensrp-ecosystem.md`
* `architecture/SYSTEM_ARCHITECTURE.md`
* `architecture/FHIR_ARCHITECTURE.md`
* `architecture/AUTHENTICATION_ARCHITECTURE.md`
* `architecture/DATA_FLOW.md`
* `architecture/DEPLOYMENT_ARCHITECTURE.md`

These documents provide the architectural and interoperability context that informs the deployment process.

---

# Contributing

Contributors making changes to deployment procedures should:

* Validate all deployment steps before committing changes.
* Keep documentation aligned with implementation.
* Record significant deployment decisions in the Architecture Decision Records (ADR) directory.
* Update this documentation whenever infrastructure changes occur.

Refer to the **oocp-governance** repository for coding standards, contribution guidelines, governance policies, and security practices.

---

# Future Enhancements

Planned improvements to the deployment process include:

* Automated installation scripts
* Infrastructure as Code with Terraform
* Kubernetes deployment manifests
* GitHub Actions deployment pipelines
* Automated security scanning
* Continuous deployment workflows
* Cloud-native deployment support
* High-availability deployment architecture

---

# Revision History

| Version | Date      | Description                                |
| ------- | --------- | ------------------------------------------ |
| 1.0.0   | July 2026 | Initial deployment documentation structure |

---

# Conclusion

The deployment documentation provides a structured path for building and operating the OpenSRP environment within the Open Oncology Care Platform. By documenting each stage of the deployment lifecycle, OOCP promotes reproducibility, maintainability, security, and standards-based interoperability, ensuring that every contributor can deploy the platform with confidence and consistency.
