# OpenSRP Ecosystem Study

**Project:** Open Oncology Care Platform (OOCP)

**Repository:** oocp-opensrp

**Author:** Stephen Maina Macharia

**Status:** Living Document

---

# 1. Purpose

This document captures the architecture, ecosystem, and engineering components that make up the Open Smart Register Platform (OpenSRP).

Rather than documenting installation steps, this document answers fundamental engineering questions:

- What is OpenSRP?
- Why was it developed?
- What problems does it solve?
- What are its major components?
- How does it support healthcare interoperability?
- How will it fit within the Open Oncology Care Platform (OOCP)?

This document will be updated throughout the project as new findings are made.

---

# 2. What is OpenSRP?

Open Smart Register Platform (OpenSRP) is an open-source, FHIR-native digital health platform designed to support healthcare workers delivering care in community and primary healthcare settings.

OpenSRP provides mobile and web applications that enable healthcare workers to register clients, manage care plans, collect structured clinical data, assign and track tasks, and monitor health programme performance. Modern versions of OpenSRP are built around HL7 FHIR standards and Google's Android FHIR SDK. :contentReference[oaicite:0]{index=0}

---

# 3. Vision

The vision of OpenSRP is to improve healthcare delivery by enabling healthcare workers to collect high-quality patient information, coordinate care, and support evidence-based decision making through interoperable digital health systems. :contentReference[oaicite:1]{index=1}

---

# 4. Core Components

The OpenSRP ecosystem is composed of several major components.

## 4.1 Android Mobile Application

Purpose:

- Community Health Workers (CHWs)
- Nurses
- Field officers
- Home visits
- Offline-first data collection
- Dynamic forms
- Synchronization with backend

Technology:

- Kotlin
- Android FHIR SDK
- MVVM Architecture
- Jetpack Compose
- Room Database

:contentReference[oaicite:2]{index=2}

---

## 4.2 FHIR Data Store

Purpose:

Acts as the source of truth for:

- Patients
- Encounters
- Observations
- Care Plans
- Tasks
- Questionnaires
- Configuration resources

OpenSRP is designed to work with a FHIR data store and supports HAPI FHIR with OpenSRP-specific extensions out of the box. :contentReference[oaicite:3]{index=3}

---

## 4.3 Identity and Access Management

Technology:

Keycloak

Responsibilities:

- Authentication
- Authorization
- OAuth2
- OpenID Connect
- User Management
- Role Management

:contentReference[oaicite:4]{index=4}

---

## 4.4 FHIR Web (Admin Dashboard)

Used by:

- Programme Managers
- Supervisors
- Administrators

Responsibilities:

- View FHIR resources
- Manage users
- Configure projects
- Monitor implementation

:contentReference[oaicite:5]{index=5}

---

## 4.5 Analytics

Supports programme monitoring and reporting by replicating transactional health data into analytics platforms such as BigQuery or other data warehouses. :contentReference[oaicite:6]{index=6}

---

# 5. High-Level Architecture

                    Community Health Worker
                             │
                             ▼
                   OpenSRP Android App
                             │
                             ▼
                     FHIR Gateway
                     (when deployed)
                             │
            ┌────────────────┴────────────────┐
            ▼                                 ▼
      HAPI FHIR Server                 Keycloak IAM
            │
            ▼
     FHIR Web Admin Dashboard
            │
            ▼
     External Systems (OOCP)

---

# 6. Role within OOCP

Within the Open Oncology Care Platform:

OpenSRP will provide the community health layer.

Responsibilities include:

- Community registration
- Oncology screening
- Referral initiation
- Follow-up
- Community surveillance
- Patient navigation

It will integrate with:

- HAPI FHIR Server
- OpenEMR
- SMART on FHIR applications
- Oncology FHIR Implementation Guide

---

# 7. Engineering Principles

The OOCP implementation of OpenSRP will follow:

- HL7 FHIR R4
- SMART on FHIR
- OAuth2
- OpenID Connect
- Clean Architecture
- SOLID Principles
- Test-Driven Development
- Docker-first deployment
- Infrastructure as Code

---

# 8. Research Questions

The following questions remain to be investigated:

- Which official repositories are required for deployment?
- How does the Android app synchronize with the FHIR server?
- How are configurations represented as FHIR resources?
- How are workflows modelled?
- How does OpenSRP support custom healthcare programmes?
- What extension points are available for oncology-specific workflows?

---

# 9. Findings Log

| Date | Finding | Source |
|------|----------|--------|
| 2026-07-25 | OpenSRP is FHIR-native and uses Android FHIR SDK. | OpenSRP Documentation |
| 2026-07-25 | HAPI FHIR acts as the primary FHIR data store. | OpenSRP Architecture |
| 2026-07-25 | Keycloak provides authentication and authorization. | OpenSRP Architecture |

---

# 10. References

1. OpenSRP Documentation
2. OpenSRP Engineering Documentation
3. HL7 FHIR R4 Specification
4. SMART on FHIR Specification
5. Keycloak Documentation
6. HAPI FHIR Documentation
