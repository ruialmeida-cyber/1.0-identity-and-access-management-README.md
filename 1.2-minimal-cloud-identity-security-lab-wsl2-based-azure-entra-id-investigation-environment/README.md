# 1.2 — Minimal Cloud & Identity Security Lab

### WSL2-Based Azure and Microsoft Entra ID Investigation Environment

**Date:** 15 January 2026
**Section:** 1.0 — Identity and Access Management
**Lab:** 1.2

---

## 1. Overview

This lab documents the design and implementation of a lightweight, reproducible cloud security investigation environment built on Windows Subsystem for Linux 2 (WSL2) using Ubuntu 24.04.

The environment is focused on Identity and Access Management (IAM) within Microsoft Azure and Microsoft Entra ID.

Rather than serving as a general-purpose development environment, the lab is designed as a controlled investigative workspace for examining authentication behaviour, identity state changes, and access control decisions in cloud-based identity systems.

The objective is to develop practical, repeatable skills in identity-focused cloud security analysis.

### Key objectives

* Establish a lightweight Linux environment for cloud security investigations.
* Develop familiarity with Azure and Microsoft Entra ID identity concepts.
* Understand authentication and access control behaviour.
* Establish a structured approach to identity investigation.
* Support repeatable, evidence-based analysis.
* Build a foundation for subsequent IAM operational labs.

---

## 2. Environment Design

The lab uses Windows Subsystem for Linux 2 (WSL2) with Ubuntu 24.04.

WSL2 provides a Linux environment that integrates with a Windows host while avoiding the overhead of maintaining a separate, full virtual machine for routine command-line investigations.

### Why WSL2?

WSL2 was selected for the following reasons:

* **Lower resource overhead:** Provides a practical Linux environment without requiring a dedicated virtual machine for every investigation.
* **Efficient execution:** Supports fast startup and repeatable command-line workflows.
* **Windows integration:** Enables interaction between Linux-based tools and Windows-based workflows.
* **CLI-driven operations:** Provides a suitable environment for scripting, automation, and technical investigation.
* **Reproducibility:** Makes it easier to document commands and repeat investigative procedures.

These characteristics make WSL2 a practical foundation for learning and experimenting with cloud identity security operations.

### Environment baseline

| Component             | Configuration                            |
| --------------------- | ---------------------------------------- |
| Host environment      | Windows                                  |
| Linux environment     | Windows Subsystem for Linux 2            |
| Linux distribution    | Ubuntu 24.04                             |
| Primary focus         | Identity and Access Management           |
| Cloud platform        | Microsoft Azure                          |
| Identity platform     | Microsoft Entra ID                       |
| Interaction model     | Command-line investigation and scripting |
| Operational objective | Repeatable identity security analysis    |

---

## 3. Identity and Access Management Focus

The central focus of this lab is understanding identity behaviour within Microsoft Entra ID and Azure authentication systems.

Identity is treated as an observable system behaviour rather than merely an administrative configuration task.

The environment provides a foundation for examining how authentication, identity state, and access decisions relate to one another.

### Areas of investigation

#### Authentication behaviour

Understanding authentication outcomes and the factors that influence whether an identity can successfully authenticate.

#### Access control decisions

Examining how identity permissions and access control mechanisms affect access to resources.

#### Identity state transitions

Understanding changes in identity state during authentication, sign-in, and session lifecycle events.

#### Identity signals and logging

Learning how authentication and identity-related activity can be represented in cloud logging systems.

#### Operational investigation

Developing a structured approach to investigating identity-related events, interpreting available evidence, and documenting conclusions.

**Scope note:** This lab establishes the investigation environment and methodology. It does not, by itself, demonstrate that a specific Azure authentication investigation has been executed or that particular Microsoft Entra ID events have been collected.

---

## 4. Investigation Workflow

Investigations should follow a structured, repeatable process.

The objective is to establish a clear relationship between the initial state, the activity being investigated, the available evidence, and the final findings.

### Standard workflow

1. **Establish the baseline**
   Identify the relevant environment, identity, configuration, or system state before beginning an investigation.

2. **Define the investigation objective**
   Specify the authentication behaviour, access decision, or identity change that needs to be examined.

3. **Collect relevant evidence**
   Use appropriate command-line tools, platform interfaces, logs, or scripts to gather information.

4. **Observe the outcome**
   Record the results of the investigation without assuming that the expected outcome occurred.

5. **Interpret the evidence**
   Relate the observed results to the investigation objective and identify any limitations.

6. **Document the findings**
   Record the commands, observations, conclusions, and relevant limitations in a consistent format.

7. **Identify the next investigative step**
   Determine whether further testing or additional evidence is required.

### Investigation principles

The workflow emphasises:

* Repeatability.
* Clear documentation.
* Evidence-based conclusions.
* Separation of observations from assumptions.
* Recognition of environmental and logging limitations.
* Avoidance of unsupported conclusions.

This approach reflects the importance of traceability and analytical discipline in cloud security operations and Security Operations Centre (SOC) workflows.

---

## 5. Technical Capabilities

This lab establishes a foundation for developing the following capabilities.

| Capability                      | Application                                               |
| ------------------------------- | --------------------------------------------------------- |
| Linux environment management    | Working within an Ubuntu-based WSL2 environment           |
| Command-line operations         | Performing technical investigations using CLI tools       |
| Microsoft Azure fundamentals    | Understanding cloud identity and access concepts          |
| Microsoft Entra ID fundamentals | Understanding identity and authentication mechanisms      |
| Authentication analysis         | Interpreting authentication outcomes and related evidence |
| Access control analysis         | Understanding permissions and access decisions            |
| Investigation methodology       | Following structured investigative workflows              |
| Scripting and automation        | Supporting repeatable technical analysis                  |
| Technical documentation         | Recording evidence, observations, and conclusions         |

These capabilities support the progression from foundational environment preparation towards more specialised IAM investigations.

---

## 6. Cloud Security Relevance

Identity is a critical component of cloud security because authentication and authorisation influence how users and other identities access resources.

A structured investigation environment provides a practical setting in which to develop the analytical skills required to understand these mechanisms.

### Relevance to cloud security operations

The environment supports the development of:

* Identity and Access Management analysis skills.
* Microsoft Azure and Entra ID operational familiarity.
* Authentication investigation techniques.
* Access control reasoning.
* Command-line investigation workflows.
* Evidence-based technical reporting.
* Repeatable investigation procedures.

These skills are relevant to identity-focused cloud security, IAM operations, and security investigation roles.

---

## 7. Security and Operational Considerations

A reproducible investigation environment should be operated with appropriate attention to security, privacy, and evidence quality.

### Least privilege

Use only the permissions necessary for the investigation. Avoid assigning elevated privileges when they are not required.

### Credential protection

Do not commit passwords, access tokens, client secrets, private keys, or other credentials to the repository.

### Data minimisation

Avoid publishing tenant identifiers, personal information, authentication details, or other sensitive information unless disclosure is necessary and authorised.

### Evidence integrity

Document what was actually observed. Distinguish between confirmed findings, assumptions, and areas that require further investigation.

### Reproducibility

Record relevant environment details and investigation steps so that procedures can be repeated and results compared.

### Scope awareness

The presence of an investigation environment does not, by itself, establish that a particular cloud investigation has been completed. Findings should be supported by the evidence collected during each exercise.

---

## 8. Relationship to the Identity and Access Management Learning Path

This lab forms part of **Section 1.0 — Identity and Access Management**.

It follows the foundational compute environment established in Lab 1.1 and introduces a Linux-based workspace for cloud identity investigation.

The wider learning path progresses from environment preparation towards identity configuration, access control validation, operational baseline analysis, identity drift investigation, and endpoint authentication behaviour.

### Learning progression

| Lab | Focus                                                 |
| --- | ----------------------------------------------------- |
| 1.1 | WSL2 Hybrid Lab Foundations                           |
| 1.2 | Minimal Cloud & Identity Security Lab                 |
| 1.3 | Entra ID Authentication and Role-Based Access Control |
| 1.4 | Entra ID Role Assignment Validation                   |
| 1.5 | Entra ID Identity Operations Baseline Validation      |
| 1.6 | Entra ID Identity Drift Analysis                      |
| 1.7 | Endpoint Authentication Behavior Analysis             |

Each lab should document its own objectives, implementation, observations, and evidence. The progression is intended to build a coherent portfolio of practical IAM work.

---

## 9. Outcome

The outcome of this lab is a lightweight, WSL2-based investigation environment designed to support structured learning and experimentation around Microsoft Azure and Microsoft Entra ID identity security.

The environment provides a foundation for developing repeatable command-line workflows, understanding cloud identity concepts, and documenting technical investigations.

Its value lies in establishing an efficient and reproducible starting point for subsequent IAM exercises.

---

## 10. Conclusion

Lab 1.2 establishes the investigation environment and working methodology needed to progress towards practical cloud identity security analysis.

By combining WSL2, Ubuntu 24.04, command-line workflows, and a structured investigative approach, the lab provides a foundation for examining authentication behaviour, access control decisions, and identity-related evidence.

It is a preparatory stage in the broader Identity and Access Management learning path, supporting progression towards more focused Microsoft Entra ID and Azure operational investigations.

---

**Section:** 1.0 — Identity and Access Management
**Lab:** 1.2 — Minimal Cloud & Identity Security Lab
**Environment:** WSL2 with Ubuntu 24.04
**Focus:** Microsoft Azure, Microsoft Entra ID, authentication analysis, and IAM investigation methodology
