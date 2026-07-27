# DEPLOYMENT_ARCHITECTURE

> **Project:** Open Oncology Care Platform (OOCP)
> **Repository:** `oocp-opensrp`
> **Document Version:** 1.0
> **Status:** Draft
> **Last Updated:** July 2026

---

# Table of Contents

1. Purpose
2. Scope
3. Deployment Objectives
4. Deployment Principles
5. High-Level Deployment Architecture
6. Infrastructure Components
7. Container Architecture
8. Network Architecture
9. Persistent Storage
10. Environment Configuration
11. Security Architecture
12. Monitoring and Logging
13. Backup and Recovery
14. Scalability Strategy
15. Future Cloud Deployment
16. References

---

# 1. Purpose

This document describes the deployment architecture of the Open Oncology Care Platform (OOCP) OpenSRP environment.

It defines how the platform will be deployed, how infrastructure components communicate, how persistent storage is managed, and how the deployment supports scalability, security, and maintainability.

This document serves as the primary infrastructure reference before implementation.

---

# 2. Scope

This document covers:

* Docker deployment
* Container architecture
* Networking
* Persistent storage
* Security
* Infrastructure services
* Monitoring
* Backup strategy
* Future cloud deployment

---

# 3. Deployment Objectives

The deployment architecture aims to:

* Provide a reproducible environment.
* Support local development.
* Support future production deployments.
* Ensure data persistence.
* Improve maintainability.
* Support container orchestration.
* Enable interoperability.
* Facilitate automated deployments.

---

# 4. Deployment Principles

The deployment follows these engineering principles:

* Infrastructure as Code (IaC)
* Container-first deployment
* Immutable infrastructure
* Configuration through environment variables
* Least privilege
* Secure defaults
* Reproducible builds
* Horizontal scalability
* Documentation-first deployment

---

# 5. High-Level Deployment Architecture

```text
                        Developer Workstation
                                │
                                ▼
                        Docker Engine
                                │
         ┌──────────────────────┼──────────────────────┐
         │                      │                      │
         ▼                      ▼                      ▼
   OpenSRP Backend         PostgreSQL             Keycloak
         │                      │                      │
         └──────────────┬───────┴───────────────┐
                        ▼                       ▼
                  Docker Network         Persistent Volumes
                        │
                        ▼
                  HAPI FHIR Server
                        │
                        ▼
                    OpenEMR
                        │
                        ▼
             SMART on FHIR Applications
```

---

# 6. Infrastructure Components

## Application Layer

* OpenSRP Backend
* Android OpenSRP Client
* SMART Applications

---

## Identity Layer

* Keycloak
* OAuth 2.0
* OpenID Connect

---

## Data Layer

* PostgreSQL
* Persistent Docker Volumes

---

## Interoperability Layer

* HAPI FHIR
* REST APIs
* HL7 FHIR R4

---

## Clinical Layer

* OpenEMR
* Oncology Implementation Guide

---

# 7. Container Architecture

The initial local deployment is expected to consist of the following containers.

| Container              | Responsibility                 |
| ---------------------- | ------------------------------ |
| OpenSRP Backend        | Business logic and REST APIs   |
| PostgreSQL             | Relational database            |
| Keycloak               | Identity and access management |
| HAPI FHIR              | FHIR server                    |
| OpenEMR                | Clinical EMR                   |
| Optional Reverse Proxy | HTTPS routing                  |
| Monitoring Services    | Metrics and observability      |

Each service is isolated within its own container while communicating over an internal Docker network.

---

# 8. Network Architecture

A dedicated Docker bridge network will connect all services.

Expected communication paths include:

* Android App → OpenSRP Backend
* OpenSRP Backend → PostgreSQL
* OpenSRP Backend → Keycloak
* OpenSRP Backend → HAPI FHIR
* OpenEMR → HAPI FHIR
* SMART Applications → HAPI FHIR

Only required services should expose ports to the host machine.

---

# 9. Persistent Storage

Persistent volumes will ensure that data survives container restarts.

Persistent storage will be allocated for:

* PostgreSQL database
* Keycloak configuration
* OpenSRP uploaded files (where applicable)
* OpenEMR data
* Logs (optional)

Volumes should be managed independently of container lifecycles.

---

# 10. Environment Configuration

Configuration should be externalised using environment variables.

Typical configuration includes:

* Database connection settings
* Authentication endpoints
* OAuth client identifiers
* FHIR server URLs
* Logging configuration
* Feature flags
* Application secrets (managed securely)

Environment-specific values (development, testing, production) should not be hard-coded.

---

# 11. Security Architecture

Deployment security controls include:

* HTTPS for external communication
* Internal Docker networking
* Secure secret management
* Non-root containers where supported
* Regular image updates
* Image vulnerability scanning
* Firewall configuration
* Role-based access to infrastructure

Sensitive credentials must never be committed to source control.

---

# 12. Monitoring and Logging

The platform should support centralised logging and monitoring.

Monitoring goals include:

* Container health
* CPU and memory usage
* API response times
* Database availability
* Authentication events
* Synchronisation status

Future tooling may include:

* Prometheus
* Grafana
* Loki
* OpenTelemetry

---

# 13. Backup and Recovery

A backup strategy should include:

* Scheduled PostgreSQL backups
* OpenEMR database backups
* Keycloak configuration exports
* Recovery testing
* Off-site backup storage (production)

Backups should be encrypted and regularly validated through restoration exercises.

---

# 14. Scalability Strategy

The architecture is designed to support future scaling.

Potential enhancements include:

* Multiple application instances
* External load balancer
* Managed PostgreSQL
* Distributed caching
* Kubernetes orchestration
* High availability deployments

---

# 15. Future Cloud Deployment

Although the initial deployment targets a local Docker environment, the architecture is intended to support cloud-native deployments.

Potential target platforms include:

* Kubernetes
* Azure Kubernetes Service (AKS)
* Amazon Elastic Kubernetes Service (EKS)
* Google Kubernetes Engine (GKE)
* OpenShift

Cloud deployments should maintain compatibility with the same architectural principles defined in this document.

---

# 16. References

The deployment architecture is informed by:

* Docker Documentation
* Docker Compose Documentation
* PostgreSQL Documentation
* Keycloak Documentation
* HAPI FHIR Documentation
* OpenSRP Documentation
* OpenEMR Documentation
* OWASP Docker Security Guidance
* CNCF Cloud Native Landscape

---

# Conclusion

The deployment architecture provides a secure, modular, and reproducible foundation for the Open Oncology Care Platform. By combining containerised services, standards-based interoperability, secure identity management, and persistent storage, the platform is designed to support both local development and future production deployments.

The architecture emphasises maintainability, portability, scalability, and healthcare interoperability while preparing the project for future cloud-native and enterprise-scale implementations.
