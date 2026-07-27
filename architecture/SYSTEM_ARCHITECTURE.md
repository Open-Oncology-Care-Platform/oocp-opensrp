# SYSTEM ARCHITECTURE

> **Project:** Open Oncology Care Platform (OOCP)
>
> **Repository:** oocp-opensrp
>
> **Document Version:** 1.0
>
> **Status:** Draft
>
> **Last Updated:** July 2026

---

# 1. Purpose

This document describes the high-level architecture of the Open Smart Register Platform (OpenSRP) within the Open Oncology Care Platform (OOCP).

Its purpose is to provide developers, architects, contributors, and healthcare professionals with a shared understanding of how OpenSRP is structured, how its components interact, and how it integrates with the broader OOCP ecosystem.

This document should be read before deployment, development, or system integration activities.

---

# 2. Scope

This document covers:

* High-level system architecture
* Core OpenSRP components
* Supporting infrastructure
* Authentication architecture
* Data flow
* External integrations
* Deployment architecture
* Future oncology extensions

Detailed deployment procedures are documented separately within the **deployment** directory.

---

# 3. Architectural Principles

The architecture of OOCP follows these principles:

* Standards-based interoperability
* Modular design
* Separation of concerns
* API-first development
* Security by design
* Documentation-first engineering
* Container-first deployment
* Cloud-ready architecture
* Open-source technologies
* Clean Architecture principles

---

# 4. System Overview

OpenSRP is a digital health platform designed primarily for community health programmes.

Within OOCP, OpenSRP acts as the **community and field-service application**, enabling healthcare workers to collect patient data, perform screening, conduct follow-up visits, and synchronise clinical information with central healthcare systems.

The platform communicates with backend services using RESTful APIs and HL7 FHIR standards wherever applicable.

---

# 5. High-Level Architecture

```text
                         +--------------------------------------+
                         |          Healthcare Workers          |
                         |        Android OpenSRP App           |
                         +------------------+-------------------+
                                            |
                                            |
                                   HTTPS / REST API
                                            |
                                            v
                         +--------------------------------------+
                         |         OpenSRP Backend API          |
                         +------------------+-------------------+
                                            |
                   +------------------------+-----------------------+
                   |                        |                       |
                   v                        v                       v
           PostgreSQL Database       Keycloak IAM         FHIR Services
                   |                        |                       |
                   +------------+-----------+-----------------------+
                                |
                                v
                    HAPI FHIR / OpenEMR Integration
                                |
                                v
                      Oncology Information Platform
```

---

# 6. Major Components

## 6.1 Android Application

The Android application is the primary interface used by healthcare workers.

Responsibilities include:

* Patient registration
* Household registration
* Clinical screening
* Follow-up visits
* Offline data capture
* Data synchronisation
* Decision support
* Task management

---

## 6.2 OpenSRP Backend

The backend coordinates all business logic.

Responsibilities include:

* User authentication
* Patient management
* Task management
* Workflow orchestration
* API endpoints
* Data validation
* Synchronisation
* Business rules

---

## 6.3 PostgreSQL

PostgreSQL stores application data.

Examples include:

* Patient records
* Tasks
* Users
* Household information
* Clinical encounters
* Synchronisation metadata
* Audit information

---

## 6.4 Keycloak

Keycloak provides identity and access management.

Responsibilities include:

* Authentication
* OAuth2
* OpenID Connect
* Token issuance
* User management
* Role management
* Single Sign-On

---

## 6.5 FHIR Layer

FHIR enables interoperability between OpenSRP and external healthcare systems.

FHIR resources may include:

* Patient
* Practitioner
* Organization
* Encounter
* Observation
* Condition
* CarePlan
* MedicationRequest

---

## 6.6 HAPI FHIR

Within OOCP, HAPI FHIR serves as the enterprise interoperability layer.

Responsibilities include:

* Resource validation
* Resource persistence
* Profile validation
* Terminology validation
* FHIR API exposure

---

## 6.7 OpenEMR

OpenEMR serves as the clinical Electronic Medical Record.

Responsibilities include:

* Clinical documentation
* Laboratory management
* Patient history
* Appointments
* Billing
* SMART on FHIR integration

---

# 7. Authentication Architecture

Authentication follows OAuth 2.0 and OpenID Connect principles.

Typical authentication flow:

1. User launches OpenSRP.
2. Credentials are submitted securely.
3. Keycloak validates identity.
4. Access token issued.
5. Backend validates token.
6. API request authorised.
7. Requested resource returned.

Future versions will support SMART on FHIR authentication where appropriate.

---

# 8. Data Flow

A typical workflow is as follows:

1. Healthcare worker registers a patient.
2. Data is stored locally (when offline).
3. Synchronisation occurs when connectivity is available.
4. Backend validates the request.
5. Data is stored in PostgreSQL.
6. FHIR resources are generated or updated.
7. HAPI FHIR exposes the data.
8. OpenEMR retrieves or exchanges relevant clinical information.
9. Oncology workflows consume interoperable data where required.

---

# 9. Security Architecture

Security is based on defence-in-depth principles.

Key controls include:

* HTTPS communication
* OAuth 2.0
* OpenID Connect
* JWT access tokens
* Role-Based Access Control (RBAC)
* Secure password storage
* Audit logging
* API authentication
* Principle of Least Privilege

---

# 10. Docker Deployment Architecture

The platform is designed to run using Docker containers.

Planned services include:

* OpenSRP Backend
* PostgreSQL
* Keycloak
* Supporting infrastructure
* Optional reverse proxy
* Monitoring services

Persistent volumes will be used for databases and application data.

---

# 11. Integration within OOCP

OpenSRP is one component of the broader Open Oncology Care Platform.

Planned integrations include:

* HAPI FHIR Server
* OpenEMR
* Oncology FHIR Implementation Guide
* SMART on FHIR applications
* Clinical decision support tools
* Community oncology workflows

---

# 12. Future Architecture

Future enhancements may include:

* Kubernetes deployment
* High availability
* Multi-site deployments
* Horizontal scaling
* FHIR Subscription support
* Event-driven architecture
* Apache Kafka integration
* AI-assisted clinical decision support
* Remote patient monitoring
* National Health Information Exchange integration

---

# 13. Architectural Decisions

Key architectural decisions will be documented separately in the `adr/` directory using Architecture Decision Records (ADRs).

---

# 14. Related Documents

* README.md
* deployment/DEPLOYMENT_PLAN.md
* research/opensrp-ecosystem.md
* Glossary.md
* OOCP Project Charter
* OOCP Roadmap

---

# 15. Revision History

| Version | Date      | Description                   | Author                |
| ------- | --------- | ----------------------------- | --------------------- |
| 1.0     | July 2026 | Initial architecture document | OOCP Engineering Team |

---

# Conclusion

The OpenSRP architecture described in this document establishes the foundation for community health workflows within the Open Oncology Care Platform. By combining OpenSRP with HAPI FHIR, OpenEMR, SMART on FHIR, and a standards-based Oncology Implementation Guide, OOCP aims to provide a modular, interoperable, secure, and scalable platform for oncology care.

This document will evolve as the platform matures and additional components, integrations, and deployment models are introduced.
