# Section 1 — Identity and Access Management (IAM)

## Overview

This repository documents practical labs focused on identity security, authentication, authorisation, and operational validation across hybrid and cloud environments.

The labs follow a structured progression, starting with the foundations of a hybrid lab environment and moving through cloud identity security, Microsoft Entra ID authentication and Role-Based Access Control (RBAC), role assignment validation, operational baseline validation, identity drift analysis, and endpoint authentication behaviour.

The objective is to develop practical skills in identity administration, access control, security validation, and investigation.

## Learning Objectives

By completing these labs, I aim to develop practical experience in:

* Establishing a hybrid lab environment using Windows Subsystem for Linux 2 (WSL2).
* Applying foundational cloud identity security principles.
* Understanding authentication and authorisation in Microsoft Entra ID.
* Investigating Azure and Entra ID role assignments.
* Validating identity operations against an established baseline.
* Identifying identity configuration drift.
* Analysing authentication behaviour at the endpoint.
* Applying least-privilege principles and documenting security findings.

## Lab Structure

The repository contains seven labs arranged in a progressive learning sequence.

### Lab 1.1 — WSL2 Hybrid Lab Foundations

**Folder:** `1.1-wsl2-hybrid-lab-foundations`

Establishes the foundational hybrid lab environment used to support subsequent identity and security investigations.

**Focus areas:**

* WSL2 environment foundations.
* Hybrid administration tooling.
* Command-line workflows.
* Preparation for subsequent identity labs.

### Lab 1.2 — Minimal Cloud Identity Security Lab

**Folder:** `1.2-minimal-cloud-identity-security-lab`

Introduces foundational cloud identity security concepts and the configuration of a minimal identity environment.

**Focus areas:**

* Cloud identity security fundamentals.
* Identity configuration.
* Security-conscious administration.
* Least-privilege principles.

### Lab 1.3 — Entra ID Authentication and Role-Based Access Control

**Folder:** `1.3-entra-id-authentication-rbac`

Explores authentication and authorisation in Microsoft Entra ID, with an emphasis on understanding how identities authenticate and how permissions govern access.

**Focus areas:**

* Microsoft Entra ID authentication.
* Role-Based Access Control (RBAC).
* Identity and access relationships.
* Authentication versus authorisation.

### Lab 1.4 — Entra ID Role Assignment Validation

**Folder:** `1.4-entra-id-role-assignment-validation`

Examines role assignments to understand how permissions are granted and whether the assignments align with the intended access configuration.

**Focus areas:**

* Role assignments.
* Role definitions and permissions.
* Assignment scope.
* Access validation.
* Least-privilege review.

### Lab 1.5 — Entra ID Identity Operations Baseline Validation

**Folder:** `1.5-entra-id-identity-operations-baseline-validation`

Validates identity operations against an established baseline after the relevant identity and access configuration work.

**Focus areas:**

* Identity configuration checks.
* Operational baseline validation.
* Role and access configuration review.
* Evidence collection.
* Identification of configuration discrepancies.

### Lab 1.6 — Entra ID Identity Drift Analysis

**Folder:** `1.6-entra-id-identity-drift-analysis`

Investigates identity configuration changes and deviations from the intended or established baseline.

**Focus areas:**

* Identity configuration drift.
* Comparison against expected state.
* Identification of unexpected changes.
* Investigation and documentation of discrepancies.
* Recommendations for maintaining configuration consistency.

### Lab 1.7 — Endpoint Authentication Behavior Analysis

**Folder:** `1.7-endpoint-authentication-behavior-analysis`

Examines authentication behaviour from the endpoint perspective to improve understanding of identity-related activity and troubleshooting.

**Focus areas:**

* Endpoint authentication behaviour.
* Authentication workflows.
* Identity-related troubleshooting.
* Security observations.
* Evidence-based investigation.

## Learning Progression

The labs are arranged in the following order:

1. **Foundations:** Prepare the hybrid lab environment.
2. **Cloud identity security:** Establish the identity-security foundations.
3. **Authentication and authorisation:** Understand how authentication and RBAC work.
4. **Role assignment validation:** Examine the permissions assigned to identities.
5. **Operational baseline validation:** Validate the resulting identity configuration.
6. **Identity drift analysis:** Investigate deviations from the intended state.
7. **Endpoint authentication analysis:** Examine authentication behaviour at the endpoint.

This sequence moves from foundational preparation to configuration, validation, investigation, and endpoint-level analysis.

## Tools and Technologies

Tools and technologies used across these labs may include:

* Microsoft Entra ID.
* Microsoft Azure.
* Azure Role-Based Access Control (RBAC).
* Windows Subsystem for Linux 2 (WSL2).
* Linux command-line tools.
* Azure CLI.
* PowerShell.
* Relevant identity and endpoint troubleshooting tools.

The specific tools used will depend on the objectives and implementation requirements of each lab.

## Security Principles

These labs emphasise the following principles:

### Least Privilege

Grant only the permissions necessary to perform the required tasks.

### Explicit Scope

Understand the scope of role assignments and the resources to which permissions apply.

### Validation Before Assumption

Verify configuration and access rather than assuming that a successful setup guarantees the intended security outcome.

### Baseline Consistency

Use an established baseline to identify configuration discrepancies and investigate unexpected changes.

### Evidence-Based Investigation

Document findings, distinguish confirmed results from assumptions, and record environmental limitations accurately.

### Protection of Sensitive Information

Do not publish credentials, access tokens, personal information, or sensitive tenant and subscription details in public documentation.

## Documentation Standards

Each lab folder should contain its own `README.md` describing:

* The lab's objective.
* The environment and tools used.
* The implementation steps.
* Commands or configurations relevant to the exercise.
* Evidence and validation results.
* Key findings.
* Lessons learned.
* Security considerations.
* Any limitations encountered.

Screenshots and other evidence may be included where appropriate, provided they do not expose sensitive information.

## Project Status

This repository is a practical learning portfolio documenting identity and access management exercises.

The status of each lab should reflect its actual implementation. Planned, partially completed, and completed work should be clearly distinguished.

## Conclusion

This collection of labs provides a structured approach to learning identity and access management across hybrid and cloud environments.

By progressing from environment foundations through authentication, RBAC, operational validation, identity drift analysis, and endpoint authentication behaviour, the project aims to build a practical understanding of identity security and access control.

The emphasis throughout is on secure configuration, validation, investigation, and clear technical documentation.
