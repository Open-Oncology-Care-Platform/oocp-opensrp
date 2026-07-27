# FHIR_ARCHITECTURE

> **Project:** Open Oncology Care Platform (OOCP)
> **Repository:** oocp-opensrp
> **Document Version:** 1.0
> **Status:** Draft
> **Last Updated:** July 2026

---

# Table of Contents

1. Purpose
2. Scope
3. Objectives
4. Why HL7 FHIR?
5. FHIR within OOCP
6. Overall FHIR Architecture
7. Core FHIR Components
8. FHIR Resource Strategy
9. FHIR Profiles
10. Terminology Services
11. Security Architecture
12. Data Exchange
13. Oncology Interoperability
14. Integration with OpenSRP
15. Integration with HAPI FHIR
16. Integration with OpenEMR
17. SMART on FHIR
18. Future Enhancements
19. References

---

# 1. Purpose

This document defines the HL7 FHIR architecture adopted by the Open Oncology Care Platform (OOCP).

It explains how healthcare information is represented, exchanged, validated, secured, and shared between OpenSRP, HAPI FHIR, OpenEMR, SMART applications, and future oncology services.

The document serves as the primary interoperability reference for the project.

---

# 2. Scope

This document covers:

* HL7 FHIR R4 architecture
* Resource modelling
* Profile strategy
* Terminology
* Security
* Data exchange
* API design
* Implementation Guide integration
* Oncology interoperability
* Future interoperability roadmap

---

# 3. Objectives

The OOCP FHIR architecture aims to:

* Promote standards-based interoperability.
* Enable secure healthcare data exchange.
* Support oncology workflows.
* Reduce vendor lock-in.
* Improve system integration.
* Encourage reusable healthcare APIs.
* Support mobile and web applications.
* Enable future national health information exchange integration.

---

# 4. Why HL7 FHIR?

FHIR (Fast Healthcare Interoperability Resources) combines modern web technologies with healthcare standards.

Key benefits include:

* RESTful APIs
* JSON and XML support
* Modular resource model
* Extensible profiles
* Strong terminology support
* Broad international adoption
* Active open-source ecosystem
* Support for mobile applications
* Compatibility with SMART on FHIR

FHIR is therefore the interoperability foundation for OOCP.

---

# 5. FHIR within OOCP

FHIR serves as the common language between all major OOCP systems.

It enables consistent representation of clinical information regardless of the source application.

Primary systems include:

* OpenSRP
* HAPI FHIR Server
* OpenEMR
* SMART Applications
* Oncology Implementation Guide
* Future AI-assisted clinical services

---

# 6. Overall FHIR Architecture

```text
                 +------------------------------+
                 |      Android OpenSRP App     |
                 +--------------+---------------+
                                |
                                |
                         REST / JSON
                                |
                                ▼
                 +------------------------------+
                 |       OpenSRP Backend        |
                 +--------------+---------------+
                                |
                         FHIR Resources
                                |
                                ▼
                 +------------------------------+
                 |      HAPI FHIR Server        |
                 +--------------+---------------+
                                |
              +-----------------+------------------+
              |                                    |
              ▼                                    ▼
        OpenEMR                         SMART Applications
              |                                    |
              +-----------------+------------------+
                                |
                                ▼
                 Oncology Information Platform
```

---

# 7. Core FHIR Components

The OOCP FHIR ecosystem consists of:

* HAPI FHIR Server
* FHIR REST API
* Resource Repository
* Terminology Validation
* Profile Validation
* Search Engine
* Security Layer
* SMART Authorization Layer

---

# 8. FHIR Resource Strategy

The platform primarily exchanges standard FHIR R4 resources.

Initial resource set:

## Administrative

* Patient
* Practitioner
* PractitionerRole
* Organization
* Location
* RelatedPerson

---

## Clinical

* Encounter
* Observation
* Condition
* Procedure
* DiagnosticReport
* MedicationRequest
* MedicationStatement
* AllergyIntolerance

---

## Oncology

* CarePlan
* CareTeam
* ServiceRequest
* Specimen
* ImagingStudy
* BodyStructure
* ClinicalImpression

---

## Workflow

* Task
* Appointment
* Communication
* DocumentReference

---

## Infrastructure

* CapabilityStatement
* StructureDefinition
* ValueSet
* CodeSystem
* NamingSystem

---

# 9. FHIR Profiles

The platform follows a profiling-first approach.

Priority profile hierarchy:

1. HL7 FHIR R4
2. National Implementation Guides (where applicable)
3. OOCP Oncology Implementation Guide
4. Local project extensions

Profiles should minimise unnecessary extensions while maintaining interoperability.

---

# 10. Terminology Services

Terminology is critical for semantic interoperability.

Preferred terminology systems include:

* SNOMED CT
* LOINC
* ICD-10
* ICD-11
* UCUM
* RxNorm (where applicable)

Responsibilities include:

* Code validation
* ValueSet expansion
* Concept mapping
* Terminology translation

---

# 11. Security Architecture

FHIR exchanges must comply with modern security practices.

Security controls include:

* HTTPS
* OAuth 2.0
* OpenID Connect
* SMART on FHIR
* JWT
* Role-Based Access Control (RBAC)
* Audit logging
* Least Privilege Principle

---

# 12. Data Exchange

The preferred communication model is RESTful FHIR APIs.

Supported operations include:

* Create
* Read
* Update
* Delete
* Search
* Conditional Create
* Conditional Update
* Batch
* Transaction

Future support:

* FHIR Messaging
* FHIR Subscriptions
* Bulk FHIR

---

# 13. Oncology Interoperability

OOCP extends standard FHIR resources using the OOCP Oncology Implementation Guide.

Planned oncology domains include:

* Cancer diagnosis
* TNM staging
* Histopathology
* Chemotherapy
* Radiotherapy
* Surgery
* Follow-up
* Survivorship
* Palliative care

The objective is to maximise interoperability while preserving clinically relevant oncology data.

---

# 14. Integration with OpenSRP

OpenSRP functions as the community-facing data collection platform.

Responsibilities include:

* Patient registration
* Community screening
* Household registration
* Follow-up activities
* Offline-first data capture
* Synchronisation with backend services

FHIR resources generated by OpenSRP should conform to approved profiles before exchange.

---

# 15. Integration with HAPI FHIR

HAPI FHIR is the primary interoperability server within OOCP.

Responsibilities include:

* Resource persistence
* Resource validation
* Profile validation
* Terminology validation
* REST API exposure
* CapabilityStatement publication

---

# 16. Integration with OpenEMR

OpenEMR serves as the clinical Electronic Medical Record.

FHIR responsibilities include:

* Clinical record exchange
* Patient synchronisation
* Encounter synchronisation
* Observation sharing
* CarePlan integration
* SMART application launch

---

# 17. SMART on FHIR

SMART on FHIR provides secure application interoperability.

Planned SMART applications include:

* Oncology Dashboard
* Chemotherapy Management
* Tumour Board Viewer
* Clinical Decision Support
* Patient Timeline
* Referral Management

Authentication will use:

* OAuth 2.0
* OpenID Connect
* PKCE
* JWT

---

# 18. Future Enhancements

The long-term FHIR roadmap includes:

* FHIR R5 evaluation
* FHIR Subscriptions
* Bulk Data Export
* CDS Hooks
* SMART Backend Services
* Clinical Quality Measures (CQM)
* Clinical Reasoning
* AI-assisted oncology decision support
* National Health Information Exchange integration

---

# 19. References

Primary standards and specifications include:

* HL7 FHIR R4
* SMART App Launch Framework
* OAuth 2.0 RFCs
* OpenID Connect Core
* HL7 Clinical Reasoning
* OOCP Oncology Implementation Guide
* HAPI FHIR Documentation
* OpenSRP Documentation
* OpenEMR FHIR Documentation

---

# Conclusion

HL7 FHIR R4 is the interoperability foundation of the Open Oncology Care Platform. By adopting internationally recognised standards, profiling resources through the OOCP Oncology Implementation Guide, and integrating OpenSRP, HAPI FHIR, OpenEMR, and SMART on FHIR, the platform aims to deliver a secure, standards-based, extensible, and interoperable digital health ecosystem for oncology care.

This architecture will evolve as the platform matures, ensuring that future enhancements remain aligned with global interoperability standards and healthcare best practices.
