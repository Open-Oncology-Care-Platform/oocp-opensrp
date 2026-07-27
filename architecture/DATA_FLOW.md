# DATA_FLOW

> **Project:** Open Oncology Care Platform (OOCP)
> **Repository:** `oocp-opensrp`
> **Document Version:** 1.0
> **Status:** Draft
> **Last Updated:** July 2026

---

# Table of Contents

1. Purpose
2. Scope
3. Objectives
4. Data Flow Principles
5. High-Level Data Flow
6. Patient Registration Workflow
7. Clinical Encounter Workflow
8. Oncology Referral Workflow
9. Synchronisation Workflow
10. FHIR Resource Lifecycle
11. Data Validation
12. Data Storage
13. Data Exchange
14. Error Handling
15. Audit Trail
16. Future Enhancements
17. References

---

# 1. Purpose

This document describes how healthcare information flows through the Open Oncology Care Platform (OOCP).

It explains how clinical data is created, validated, stored, synchronised, transformed into FHIR resources, exchanged with external systems, and ultimately consumed by healthcare providers.

---

# 2. Scope

This document covers the flow of healthcare data between:

* Android OpenSRP Application
* OpenSRP Backend
* PostgreSQL
* Keycloak
* HAPI FHIR Server
* OpenEMR
* SMART on FHIR Applications
* Oncology Implementation Guide

---

# 3. Objectives

The OOCP data flow architecture is designed to:

* Ensure accurate healthcare data capture.
* Maintain data integrity.
* Enable standards-based interoperability.
* Support offline-first workflows.
* Reduce duplicate data entry.
* Provide secure data exchange.
* Improve clinical decision-making.
* Support future national health information exchange.

---

# 4. Data Flow Principles

All healthcare data should follow these principles:

* Capture data once.
* Reuse data wherever possible.
* Validate before storage.
* Exchange using HL7 FHIR.
* Encrypt data in transit.
* Maintain audit trails.
* Preserve clinical integrity.
* Minimise manual intervention.

---

# 5. High-Level Data Flow

```text
                    Community Health Worker
                               │
                               ▼
                    Android OpenSRP Application
                               │
                 (Offline or Online Data Capture)
                               │
                               ▼
                      OpenSRP Backend API
                               │
              Authentication & Business Validation
                               │
                               ▼
                         PostgreSQL Database
                               │
                    Resource Transformation
                               │
                               ▼
                        HL7 FHIR Resources
                               │
                               ▼
                        HAPI FHIR Server
                               │
              +----------------+----------------+
              |                                 |
              ▼                                 ▼
         OpenEMR                      SMART Applications
              |                                 |
              +----------------+----------------+
                               │
                               ▼
                    Oncology Care Platform
```

---

# 6. Patient Registration Workflow

The following sequence describes the registration of a new patient.

### Step 1 – User Authentication

The healthcare worker authenticates using OAuth 2.0/OpenID Connect.

---

### Step 2 – Patient Registration

The healthcare worker records:

* Demographics
* Contact information
* Household information
* Location
* Clinical identifiers

---

### Step 3 – Local Validation

The mobile application validates:

* Required fields
* Data types
* Duplicate identifiers
* Business rules

---

### Step 4 – Local Storage

If the device is offline, data is securely stored locally until connectivity is restored.

---

### Step 5 – Synchronisation

When connectivity becomes available:

* Data is transmitted securely.
* Authentication token is verified.
* Backend validation occurs.

---

### Step 6 – Database Persistence

Validated information is stored within PostgreSQL.

---

### Step 7 – FHIR Resource Generation

The patient record is converted into a FHIR **Patient** resource and linked resources where appropriate.

---

### Step 8 – Interoperability

The resource becomes available through the HAPI FHIR Server for authorised systems.

---

# 7. Clinical Encounter Workflow

During a patient visit:

1. Retrieve patient.
2. Create Encounter.
3. Record Observations.
4. Record Conditions.
5. Update CarePlan.
6. Save clinical notes.
7. Validate data.
8. Synchronise.
9. Generate FHIR resources.
10. Publish to HAPI FHIR.

---

# 8. Oncology Referral Workflow

Future oncology referrals will include:

* Referral initiation
* Cancer diagnosis
* Histopathology
* TNM staging
* Treatment recommendation
* Referral acceptance
* Care coordination
* Follow-up scheduling

FHIR resources involved include:

* ServiceRequest
* Condition
* CarePlan
* DiagnosticReport
* Observation
* Task

---

# 9. Synchronisation Workflow

OpenSRP follows an offline-first approach.

The synchronisation engine is responsible for:

* Uploading pending records.
* Downloading updates.
* Resolving conflicts.
* Tracking synchronisation status.
* Preventing duplicate submissions.
* Maintaining transaction consistency.

---

# 10. FHIR Resource Lifecycle

Healthcare information progresses through the following lifecycle:

```text
Clinical Observation
        │
        ▼
Business Validation
        │
        ▼
FHIR Resource Creation
        │
        ▼
Profile Validation
        │
        ▼
Terminology Validation
        │
        ▼
FHIR Repository
        │
        ▼
FHIR REST API
        │
        ▼
External Healthcare Systems
```

---

# 11. Data Validation

Validation occurs at multiple levels:

### Client Validation

* Mandatory fields
* Data types
* User interface constraints

### Backend Validation

* Business rules
* Clinical consistency
* Duplicate detection
* Security validation

### FHIR Validation

* Resource structure
* Profile conformance
* Cardinality
* Terminology validation

---

# 12. Data Storage

Primary data storage:

* PostgreSQL

Interoperability storage:

* HAPI FHIR Server

Clinical record management:

* OpenEMR

Future analytics repositories may support reporting and research while respecting governance and privacy requirements.

---

# 13. Data Exchange

Primary exchange mechanism:

* HTTPS
* REST APIs
* JSON
* HL7 FHIR R4

Future mechanisms:

* FHIR Messaging
* FHIR Subscriptions
* Bulk FHIR Export
* Event-driven integration

---

# 14. Error Handling

Potential failures include:

* Network interruptions
* Authentication failures
* Validation errors
* Duplicate records
* Synchronisation conflicts
* Server failures

The platform should:

* Retry transient operations.
* Record detailed logs.
* Preserve local data.
* Notify users appropriately.
* Prevent data loss.

---

# 15. Audit Trail

All significant data events should be recorded, including:

* Patient creation
* Patient updates
* Clinical documentation
* Synchronisation events
* FHIR resource creation
* User logins
* Administrative changes

Audit records should include:

* User identity
* Timestamp
* Action performed
* Target resource
* Outcome

---

# 16. Future Enhancements

Future improvements include:

* Real-time event streaming
* FHIR Subscriptions
* Clinical Decision Support (CDS Hooks)
* AI-assisted oncology workflows
* National Health Information Exchange integration
* Population health analytics
* Remote patient monitoring
* Distributed event architecture

---

# 17. References

The data flow architecture aligns with:

* HL7 FHIR R4
* SMART App Launch Framework
* OAuth 2.0
* OpenID Connect
* OpenSRP Documentation
* HAPI FHIR Documentation
* OpenEMR Documentation
* OWASP Secure Coding Practices

---

# Conclusion

The Open Oncology Care Platform adopts a secure, standards-based, and interoperability-first data flow architecture. Clinical information is captured once, validated throughout its lifecycle, transformed into HL7 FHIR resources, and securely exchanged between OpenSRP, HAPI FHIR, OpenEMR, SMART on FHIR applications, and future oncology services.

By emphasising data quality, auditability, offline-first operation, and adherence to international interoperability standards, the platform provides a strong foundation for scalable and patient-centred oncology care.
