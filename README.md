# OpenSRP for the Open Oncology Care Platform (OOCP)

## Overview

This repository contains the OpenSRP deployment, configuration, documentation, and customization work for the **Open Oncology Care Platform (OOCP)**.

OpenSRP (Open Smart Register Platform) is an open-source digital health platform designed to support community health programmes through mobile-first workflows. Within OOCP, OpenSRP serves as the **community health layer**, enabling Community Health Workers (CHWs) to collect, manage, and synchronize patient information from the field using standardized healthcare interoperability technologies.

The objective of this repository is not only to deploy OpenSRP but also to study its architecture, understand its interoperability capabilities, and customize it for oncology care workflows.

---

# Project Objectives

This repository aims to:

- Deploy the latest stable version of OpenSRP using Docker.
- Understand the internal architecture of OpenSRP.
- Study how OpenSRP exchanges healthcare information using HL7 FHIR R4.
- Integrate OpenSRP with the OOCP interoperability platform.
- Develop oncology-specific community screening workflows.
- Document every engineering decision and implementation step.
- Produce a reproducible deployment suitable for research, education, and software engineering portfolios.

---

# Why OpenSRP?

Cancer care begins long before a patient reaches a hospital.

Many cancer control programmes rely heavily on community health workers to:

- Conduct household visits.
- Perform health education.
- Identify high-risk individuals.
- Conduct cancer screening.
- Refer suspected cases to healthcare facilities.
- Follow up patients undergoing treatment.

OpenSRP was designed specifically to support these community-based healthcare workflows.

Unlike traditional Electronic Medical Record (EMR) systems, OpenSRP focuses on **frontline healthcare delivery**, making it an ideal platform for community oncology programmes.

---

# OpenSRP within the OOCP Architecture

Within the Open Oncology Care Platform, OpenSRP represents the first point of contact between the patient and the healthcare system.

```text
Community Health Worker

        │

        ▼

OpenSRP Mobile Application

        │

        ▼

OpenSRP Backend

        │

        ▼

HAPI FHIR Server

        │

        ▼

OpenEMR

        │

        ▼

SMART on FHIR Applications

        │

        ▼

Clinical Analytics
```

This architecture enables standardized data exchange throughout the continuum of cancer care.

---

# Why HL7 FHIR?

The Open Oncology Care Platform adopts **HL7 FHIR R4** as its interoperability standard.

FHIR enables healthcare systems to exchange structured clinical information using standard resources such as:

- Patient
- Encounter
- Observation
- Condition
- Procedure
- CarePlan
- MedicationRequest
- ServiceRequest
- Questionnaire
- QuestionnaireResponse

Using FHIR ensures interoperability between OpenSRP, OpenEMR, HAPI FHIR, SMART applications, and future healthcare systems.

---

# Why Docker?

Docker provides:

- Reproducible deployments.
- Environment isolation.
- Simplified dependency management.
- Portable development environments.
- Easier onboarding for contributors.

All OpenSRP services within this repository will be containerized to ensure consistent deployments across different operating systems.

---

# Repository Structure

```
oocp-opensrp/

├── README.md
├── docs/
├── research/
├── deployment/
├── diagrams/
├── adr/
├── scripts/
└── notes/
```

## Folder Description

### docs/

Contains project documentation including:

- Installation Guide
- Configuration Guide
- Authentication Guide
- API Documentation
- Deployment Guide

---

### research/

Contains technical study notes produced during the project, including:

- OpenSRP Architecture
- FHIR Integration
- Authentication
- Synchronization
- Android Client
- Data Model

---

### deployment/

Contains deployment-related artefacts including:

- Docker Compose
- Environment configuration
- Database initialization
- Deployment scripts

---

### diagrams/

Contains software engineering diagrams including:

- System Context Diagram
- Container Diagram
- Component Diagram
- Deployment Diagram
- Sequence Diagrams

---

### adr/

Architecture Decision Records documenting important engineering decisions.

Examples include:

- Why OpenSRP was selected.
- Why Docker was adopted.
- Why PostgreSQL was selected.
- Why HL7 FHIR R4 is the interoperability standard.

---

### scripts/

Automation scripts used throughout the project.

Examples:

- Environment setup
- Backup
- Restore
- Database reset
- Docker automation

---

### notes/

Engineering notebook containing:

- Learning notes
- Troubleshooting
- Future ideas
- Observations

---

# Technologies

The OpenSRP component of OOCP will utilise the following technologies:

| Component | Technology |
|------------|------------|
| Community Health Platform | OpenSRP |
| Backend | Spring Boot |
| Authentication | Keycloak |
| Database | PostgreSQL |
| Containerization | Docker |
| Interoperability | HL7 FHIR R4 |
| Security | OAuth 2.0 + OpenID Connect |
| API Testing | Postman |
| Version Control | Git |
| Continuous Integration | GitHub Actions |

---

# Planned Learning Outcomes

By the completion of this repository, contributors should understand:

- OpenSRP architecture.
- Community health workflows.
- OpenSRP deployment.
- Docker orchestration.
- Keycloak authentication.
- HL7 FHIR interoperability.
- SMART on FHIR integration.
- Community oncology workflows.
- Software engineering best practices.
- Healthcare interoperability principles.

---

# Repository Roadmap

Phase 1

- Repository setup
- Documentation
- Docker environment

Phase 2

- OpenSRP deployment

Phase 3

- Authentication and authorization

Phase 4

- FHIR interoperability

Phase 5

- Community oncology workflows

Phase 6

- Integration with HAPI FHIR

Phase 7

- Integration with OpenEMR

Phase 8

- SMART on FHIR applications

Phase 9

- Production-ready deployment

---

# Engineering Principles

Development within this repository follows the engineering standards defined by the Open Oncology Care Platform Governance.

These principles include:

- Clean Architecture
- SOLID Principles
- Test-Driven Development (TDD)
- Clean Code (Robert C. Martin)
- The Pragmatic Programmer principles
- Continuous Integration
- Continuous Documentation
- Security by Design
- Infrastructure as Code
- Healthcare Interoperability by Design

---

# References

This repository is informed by internationally recognised standards and projects, including:

- HL7 FHIR Release 4 (R4)
- SMART on FHIR
- OpenSRP
- OpenMRS
- OpenEMR
- OAuth 2.0
- OpenID Connect
- Docker
- PostgreSQL
- Spring Boot
- OWASP Secure Coding Practices

---

# License

This repository is part of the **Open Oncology Care Platform (OOCP)** and is released under the project's open-source license.

---

# Author

**Stephen Maina Macharia**

Founder, Open Oncology Care Platform (OOCP)

Healthcare Interoperability Engineer | Software Engineer | Occupational Safety & Health Professional

---

> **Mission:** To build an open, standards-based oncology platform that demonstrates how modern digital health systems can support the complete continuum of cancer care—from community screening to hospital treatment—using HL7 FHIR R4, SMART on FHIR, and open-source technologies.
