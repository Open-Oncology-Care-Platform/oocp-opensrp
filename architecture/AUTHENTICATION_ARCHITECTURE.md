# AUTHENTICATION_ARCHITECTURE

> **Project:** Open Oncology Care Platform (OOCP)
> **Repository:** `oocp-opensrp`
> **Document Version:** 1.0
> **Status:** Draft
> **Last Updated:** July 2026

---

# Table of Contents

1. Purpose
2. Scope
3. Authentication Objectives
4. Security Principles
5. Identity Architecture
6. Authentication Components
7. Authentication Flow
8. Authorization Model
9. OAuth 2.0
10. OpenID Connect (OIDC)
11. SMART on FHIR Authentication
12. JWT Token Architecture
13. Role-Based Access Control (RBAC)
14. API Security
15. Session Management
16. Password Policy
17. Audit Logging
18. Future Authentication Enhancements
19. References

---

# 1. Purpose

This document defines the authentication and authorization architecture of the Open Oncology Care Platform (OOCP).

It describes how users, applications, and services authenticate, obtain access to protected resources, and securely exchange healthcare information while complying with modern cybersecurity best practices.

---

# 2. Scope

This document covers:

* User authentication
* Service authentication
* OAuth 2.0
* OpenID Connect (OIDC)
* SMART on FHIR
* JWT token management
* Role-Based Access Control (RBAC)
* API security
* Session management
* Future authentication strategy

---

# 3. Authentication Objectives

The authentication architecture is designed to:

* Protect patient information.
* Ensure only authorised users access healthcare data.
* Support secure application-to-application communication.
* Enable interoperability using SMART on FHIR.
* Support Single Sign-On (SSO).
* Minimise credential exposure.
* Follow Zero Trust principles.
* Scale across multiple healthcare systems.

---

# 4. Security Principles

The authentication architecture is based on the following principles:

* Zero Trust
* Least Privilege
* Defence in Depth
* Secure by Design
* Identity First
* Standards-Based Authentication
* Token-Based Authorization
* Principle of Separation of Duties

---

# 5. Identity Architecture

OOCP separates **Identity Management** from **Business Logic**.

The Identity Provider (IdP) is responsible for:

* User authentication
* Password management
* Token generation
* Session management
* Multi-factor authentication (future)
* Identity federation
* Single Sign-On (SSO)

Business applications consume identity information but do not manage user credentials directly.

---

# 6. Authentication Components

The planned authentication ecosystem consists of:

* Android OpenSRP Application
* OpenSRP Backend
* Keycloak Identity Provider
* OAuth 2.0 Authorization Server
* OpenID Connect Provider
* HAPI FHIR Server
* OpenEMR
* SMART on FHIR Applications

---

# 7. High-Level Authentication Architecture

```text
                  +----------------------------+
                  |   Healthcare Professional  |
                  +-------------+--------------+
                                |
                                ▼
                     Android / Web Application
                                |
                                ▼
                         OAuth 2.0 Login
                                |
                                ▼
                     +----------------------+
                     |      Keycloak        |
                     | Identity Provider    |
                     +----------+-----------+
                                |
                     Authentication Success
                                |
                                ▼
                     Access Token (JWT)
                                |
                                ▼
                     OpenSRP Backend API
                                |
                 +--------------+--------------+
                 |                             |
                 ▼                             ▼
           HAPI FHIR                     OpenEMR
```

---

# 8. Authentication Flow

The standard authentication process is:

1. User opens the application.
2. Login request is redirected to the Identity Provider.
3. Credentials are validated.
4. OAuth 2.0 authorization is completed.
5. An OpenID Connect ID Token is generated.
6. A JWT Access Token is issued.
7. The client stores the token securely.
8. API requests include the Bearer Token.
9. Backend services validate the token.
10. Access is granted based on assigned roles and permissions.

---

# 9. Authorization Model

Authentication confirms **who the user is**.

Authorization determines **what the user is allowed to do**.

The OOCP platform uses Role-Based Access Control (RBAC) with fine-grained permissions enforced by backend services.

---

# 10. OAuth 2.0

OAuth 2.0 provides delegated authorization between clients and protected resources.

Supported grant types (planned):

* Authorization Code with PKCE
* Client Credentials
* Refresh Token

Deprecated grant types such as the Implicit Flow will not be used.

---

# 11. OpenID Connect (OIDC)

OIDC extends OAuth 2.0 by adding authentication and identity information.

OOCP will use OIDC for:

* User identity verification
* Single Sign-On
* Standard user claims
* Identity federation

---

# 12. SMART on FHIR Authentication

SMART on FHIR enables secure healthcare applications to interact with FHIR servers.

Planned authentication flow:

1. SMART application requests authorisation.
2. User authenticates via Keycloak.
3. OAuth 2.0 Authorization Code Flow with PKCE is executed.
4. Access Token and ID Token are issued.
5. SMART application accesses authorised FHIR resources.

---

# 13. JWT Token Architecture

JWT Access Tokens will contain claims such as:

* Subject (sub)
* Issuer (iss)
* Audience (aud)
* Expiration (exp)
* Issued At (iat)
* Roles
* Scopes

Tokens should be:

* Digitally signed
* Short-lived
* Validated on every request
* Never logged in plain text

---

# 14. Role-Based Access Control (RBAC)

The following roles are planned:

### Community Health Worker

Permissions:

* Register patients
* Record visits
* Capture observations
* View assigned patients

---

### Nurse

Additional permissions:

* Review patient records
* Manage appointments
* Update clinical information

---

### Clinician

Additional permissions:

* Diagnose conditions
* Create CarePlans
* Request investigations
* Prescribe treatment

---

### Oncologist

Additional permissions:

* Manage oncology cases
* Record cancer staging
* Develop treatment plans
* Review multidisciplinary team recommendations

---

### Administrator

Permissions:

* User management
* Role assignment
* System configuration
* Audit review

---

# 15. API Security

All APIs must:

* Require HTTPS
* Validate JWT tokens
* Enforce scopes and roles
* Return standard HTTP status codes
* Implement rate limiting (future)
* Record security audit events

---

# 16. Session Management

Security controls include:

* Short-lived Access Tokens
* Refresh Tokens
* Secure token storage
* Session timeout
* Automatic logout after inactivity
* Token revocation support

---

# 17. Password Policy

Recommended requirements:

* Minimum 12 characters
* Uppercase and lowercase letters
* Numbers
* Special characters
* Password history enforcement
* Password expiration (policy dependent)
* Account lockout after repeated failed attempts

Where possible, Multi-Factor Authentication (MFA) should be enabled for privileged users.

---

# 18. Audit Logging

Authentication-related events to record include:

* Successful logins
* Failed login attempts
* Password changes
* Role assignments
* Token issuance
* Token revocation
* Privileged operations
* Administrative actions

Audit logs should be immutable and retained according to organisational policy.

---

# 19. Future Authentication Enhancements

Planned enhancements include:

* Multi-Factor Authentication (MFA)
* Biometric authentication on supported mobile devices
* Identity federation with national identity providers
* Hardware security keys (FIDO2/WebAuthn)
* Risk-based authentication
* Adaptive access policies
* Device trust management

---

# References

This architecture is informed by:

* HL7 FHIR R4 Security guidance
* SMART App Launch Framework
* OAuth 2.0 specifications
* OpenID Connect Core
* OWASP Authentication Cheat Sheet
* OWASP API Security Top 10
* NIST Digital Identity Guidelines (SP 800-63)
* Keycloak Documentation

---

# Conclusion

The authentication architecture of the Open Oncology Care Platform is built on internationally recognised identity and security standards. By adopting OAuth 2.0, OpenID Connect, SMART on FHIR, JWT-based authentication, and Role-Based Access Control, OOCP establishes a secure and scalable identity foundation for interoperable oncology care.

As the platform evolves, this architecture will expand to incorporate advanced identity capabilities such as Multi-Factor Authentication, federation with external identity providers, and adaptive authentication while maintaining compatibility with healthcare interoperability standards.
