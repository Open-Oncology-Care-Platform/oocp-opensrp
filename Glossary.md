# GLOSSARY

**Project:** Open Oncology Care Platform (OOCP)

**Repository:** oocp-project-specification

**Version:** 1.0.0

**Status:** Living Document

---

# Purpose

This glossary defines the terminology used throughout the Open Oncology Care Platform (OOCP).

It provides a common vocabulary for contributors, developers, healthcare professionals, researchers, and architects involved in the project.

As the project evolves, new terms will be added and existing definitions refined.

---

# How to Use This Glossary

* Definitions are organised alphabetically.
* Acronyms are listed using their official names.
* Where appropriate, definitions reference recognised healthcare or software engineering standards.
* This document should be updated whenever new terminology is introduced into the project.

---

# A

## ADR (Architecture Decision Record)

A document that captures an important architectural decision, the context in which it was made, the alternatives considered, and the rationale for the final decision.

---

## API (Application Programming Interface)

A defined set of rules that allows software applications to communicate with one another.

---

## Apache License 2.0

A permissive open-source software licence allowing users to use, modify, and distribute software under defined conditions.

---

## Authentication

The process of verifying the identity of a user, application, or system.

---

## Authorization

The process of determining what an authenticated user or system is permitted to access.

---

# C

## CarePlan

A HL7 FHIR resource that represents a patient's planned healthcare activities, goals, interventions, and follow-up actions.

---

## CI/CD (Continuous Integration / Continuous Delivery)

A software engineering practice that automates building, testing, and deploying software.

---

## Clean Architecture

A software architecture approach proposed by Robert C. Martin that separates business logic from implementation details to improve maintainability and testability.

---

## Clean Code

A software engineering philosophy introduced by Robert C. Martin that emphasises readability, simplicity, maintainability, and professionalism in software development.

---

## Clinical Decision Support (CDS)

Software that provides healthcare professionals with patient-specific knowledge and recommendations to improve clinical decision-making.

---

## Community Health Worker (CHW)

A trained healthcare worker who provides preventive, promotive, and basic healthcare services within communities.

---

# D

## DevOps

A set of practices that combines software development and IT operations to improve software delivery and reliability.

---

## Docker

A containerisation platform used to package and deploy applications consistently across different environments.

---

## Docker Compose

A tool used to define and manage multi-container Docker applications.

---

## Domain-Driven Design (DDD)

A software development methodology that models software around the business domain it serves.

---

# E

## Electronic Medical Record (EMR)

A digital version of a patient's medical record maintained by a healthcare organisation.

---

## Evidence-Based Engineering

An engineering approach that prioritises decisions supported by recognised standards, research, best practices, and empirical evidence.

---

# F

## FHIR (Fast Healthcare Interoperability Resources)

An international interoperability standard developed by HL7 for exchanging healthcare information using modern web technologies.

---

## FHIR Server

A server implementation capable of storing, validating, and exchanging FHIR resources through standard RESTful APIs.

---

## FHIR Resource

The fundamental building block of the FHIR standard representing a specific healthcare concept such as a Patient, Observation, Encounter, or Medication.

---

# G

## Git

A distributed version control system used to manage software source code and documentation.

---

## GitHub

A cloud-based platform for hosting Git repositories and enabling collaborative software development.

---

# H

## HAPI FHIR

An open-source Java implementation of the HL7 FHIR standard providing client libraries and a production-ready FHIR server.

---

## HL7 (Health Level Seven)

An international standards organisation responsible for developing interoperability standards for healthcare information exchange.

---

# I

## Implementation Guide (IG)

A formal specification that describes how HL7 FHIR should be implemented for a specific healthcare domain or use case.

---

## Infrastructure as Code (IaC)

The practice of managing infrastructure using version-controlled configuration files instead of manual processes.

---

## Interoperability

The ability of different healthcare information systems to exchange and correctly interpret shared information.

---

# J

## JWT (JSON Web Token)

A compact, digitally signed token commonly used to securely exchange identity and authorisation information.

---

# K

## Keycloak

An open-source Identity and Access Management (IAM) platform providing authentication, authorisation, and single sign-on capabilities.

---

# O

## OAuth 2.0

An industry-standard authorisation framework that enables secure delegated access between applications.

---

## Oncology

The branch of medicine concerned with the prevention, diagnosis, treatment, and management of cancer.

---

## OOCP (Open Oncology Care Platform)

An open-source initiative focused on building a standards-based, interoperable oncology platform using modern healthcare technologies and software engineering best practices.

---

## OpenEMR

An open-source electronic medical record and practice management system supporting HL7 FHIR APIs and SMART on FHIR integration.

---

## OpenID Connect (OIDC)

An identity layer built on top of OAuth 2.0 that enables applications to verify user identities securely.

---

## OpenSRP (Open Smart Register Platform)

An open-source digital health platform designed to support community health programmes, field workers, and population health management.

---

# P

## PostgreSQL

An open-source relational database management system widely used in enterprise software and healthcare applications.

---

## Practitioner

A HL7 FHIR resource representing a healthcare professional involved in providing care.

---

## Patient

A HL7 FHIR resource representing an individual receiving healthcare services.

---

## PKCE (Proof Key for Code Exchange)

An extension to OAuth 2.0 that protects public clients, such as mobile and browser applications, against authorisation code interception attacks.

---

# R

## Repository

A version-controlled storage location containing source code, documentation, configuration files, or other project artefacts.

---

## REST (Representational State Transfer)

An architectural style for designing web services that communicate using standard HTTP methods.

---

# S

## SMART on FHIR

A standard that enables secure healthcare applications to integrate with FHIR servers using OAuth 2.0 and OpenID Connect.

---

## SOLID Principles

Five object-oriented design principles that promote maintainable, extensible, and robust software systems.

---

## Semantic Versioning

A version numbering convention using the format **MAJOR.MINOR.PATCH** to communicate software changes.

---

## Software Architecture

The high-level structure of a software system, including its components, interactions, technologies, and design principles.

---

# T

## Test-Driven Development (TDD)

A software development practice in which automated tests are written before production code.

---

## Terminology Server

A specialised server that manages healthcare code systems, value sets, concept maps, and terminology validation.

---

# U

## UML (Unified Modeling Language)

A standard visual modelling language used to represent software architecture, behaviour, and system design.

---

# V

## ValueSet

A HL7 FHIR resource defining a collection of codes drawn from one or more code systems for use in healthcare data exchange.

---

## Version Control

A system that records changes to files over time, enabling collaboration, history tracking, and rollback.

---

# W

## Workflow

A defined sequence of activities or business processes performed to achieve a specific healthcare or engineering objective.

---

# Future Additions

This glossary will continue to expand throughout the project and is expected to include terminology related to:

* Kubernetes
* Terraform
* SNOMED CT
* LOINC
* ICD-10
* ICD-11
* DICOM
* PACS
* Mirth Connect
* RabbitMQ
* Kafka
* GraphQL
* CQRS
* Event Sourcing
* Microservices
* FHIR Subscriptions
* CDS Hooks
* Bulk FHIR
* SMART Backend Services
* OpenHIM
* OpenMRS
* OpenELIS
* DHIS2
* OpenCRVS

---

# Maintenance

This glossary is a living document.

Every new technical term introduced into the Open Oncology Care Platform should be defined here before it is used extensively elsewhere in the project. Maintaining a consistent vocabulary improves communication, documentation quality, and long-term maintainability across the entire OOCP ecosystem.
