# Lab 1.1 — WSL2 Hybrid Lab Foundations

**Category:** Identity and Access Management (IAM)
**Focus:** Foundational compute environment for cloud and identity security learning
**Date:** January 2026

---

## Overview

This project establishes a constrained compute environment designed to simulate foundational infrastructure conditions relevant to identity and cloud security operations.

Originally initiated as a hardware recovery and system optimisation exercise, the environment was repurposed into a structured security lab for developing operational familiarity with Linux systems, command-line administration, and security tooling under resource constraints.

From an Identity and Access Management (IAM) perspective, this environment represents the foundational compute layer supporting later identity-focused analysis, including authentication workflows, Role-Based Access Control (RBAC) concepts, and Microsoft Entra ID-aligned identity governance scenarios.

The system provides a preparatory environment for understanding how identity, authentication, and system access interact with underlying infrastructure in lightweight and constrained computing contexts.

## Objectives

The objectives of this lab are to:

* Establish a stable Linux-based security lab environment.
* Develop familiarity with command-line system administration.
* Explore security tooling on resource-constrained hardware.
* Understand foundational Linux permissions and user-management concepts.
* Prepare a reproducible environment for subsequent identity and cloud security labs.
* Establish a practical foundation for investigating authentication and access control.

## System Constraints and Baseline Context

The system operates under legacy hardware limitations.

| Component         | Configuration or condition                                                       |
| ----------------- | -------------------------------------------------------------------------------- |
| Memory            | 4 GB DDR3 RAM                                                                    |
| Firmware          | Legacy BIOS architecture; no UEFI support                                        |
| Storage           | SATA SSD upgrade replacing a failing HDD                                         |
| Connectivity      | USB 2.0 interface limitations                                                    |
| Thermal condition | Initial thermal instability addressed through cleaning and hardware optimisation |

These constraints provide a practical opportunity to observe how system performance affects command-line administration and security tooling.

They also offer useful context when considering lightweight virtual machines and minimal cloud compute instances, although a physical laptop and a cloud virtual machine have different architectural and operational characteristics.

## Security Environment Design

### Operating System

MX Linux was selected because of its efficiency, stability, and compatibility with legacy hardware.

The Linux environment supports:

* Command-line system administration.
* Lightweight security tooling.
* Foundational Linux permissions and user-management concepts.
* Terminal-based workflows relevant to cloud administration.
* Scripting and repeatable operational tasks.

### Relevance to Identity and Cloud Security

A reliable compute environment is an important foundation for security learning and investigation.

Although this lab does not itself implement Microsoft Entra ID authentication or Azure RBAC, it develops the operational familiarity needed to work with command-line tools and investigate security-related behaviour in subsequent labs.

## Security Tooling Baseline

The following tools were configured to support foundational security analysis.

| Security area                   | Tools                 |
| ------------------------------- | --------------------- |
| Network visibility and scanning | Nmap, Wireshark       |
| System auditing                 | Lynis                 |
| Endpoint protection concepts    | ClamAV, Fail2ban, UFW |
| Scripting and automation        | Python 3, Git         |

These tools provide a starting point for network inspection, system auditing, endpoint protection concepts, and automation.

Their presence in the environment does not by itself establish that every security control is enabled or that the system has been comprehensively hardened. Configuration and validation remain necessary for each tool.

## Implementation and Optimisation

The project began as a hardware recovery and system optimisation exercise.

The main areas of work included:

1. Addressing the failing hard drive by replacing it with a SATA SSD.
2. Cleaning the system and addressing the initial thermal instability.
3. Installing and configuring MX Linux for the available hardware.
4. Establishing a command-line environment for administration and security tooling.
5. Preparing the system for repeatable security learning activities.

The objective was to create a usable and stable environment despite the limitations of the legacy hardware.

## Observations

System optimisation through the SSD upgrade and operating-system tuning resulted in:

* More stable boot performance.
* Improved system responsiveness.
* More reliable execution of command-line security workflows.
* Reduced system instability under workload conditions.

These observations demonstrate the practical value of maintaining a stable compute environment before introducing more complex security tasks.

Performance improvements were observed in this specific system and should not be treated as a direct benchmark for cloud infrastructure.

## Learning Outcomes

This project developed foundational capabilities relevant to identity and cloud security operations.

Key learning outcomes include:

* Understanding system behaviour under constrained compute conditions.
* Performing Linux administration through command-line workflows.
* Using security tools within a resource-limited environment.
* Establishing a structured environment for repeatable lab activities.
* Recognising the relationship between underlying infrastructure and security operations.
* Preparing for identity lifecycle, authentication, and access-control investigations.

## IAM and Cloud Security Context

This lab establishes the foundational compute environment for the wider Identity and Access Management learning path.

It provides operational context for subsequent work involving Microsoft Entra ID and Azure identity services.

The environment supports progression towards identity-centric security analysis, including:

* Authentication behaviour.
* Access-control interpretation.
* Identity lifecycle concepts.
* Command-line investigation workflows.
* Security configuration validation.

The distinction between the underlying compute environment and cloud identity services is important: this lab prepares the environment and foundational skills, while later labs investigate identity and access management directly.

## Security Considerations

The lab emphasises several practical considerations:

* **System stability:** Resolve underlying hardware or operating-system issues before relying on the environment for security investigations.
* **Tool validation:** Confirm that security tools are configured and operating as intended rather than assuming installation alone provides protection.
* **Resource awareness:** Consider memory, storage, and processing limitations when running security tools.
* **Reproducibility:** Document configurations and workflows so that lab activities can be repeated.
* **Separation of responsibilities:** Distinguish local operating-system administration from cloud identity and authorisation management.

## Outcome

The legacy system was converted into a stable Linux-based security lab environment.

It now serves as a foundational platform supporting progression into:

* Microsoft Entra ID identity and access management.
* Azure cloud administration and security.
* Identity-driven security analysis.
* Authentication and access-control investigations.
* Further command-line security and operational validation exercises.

## Conclusion

Lab 1.1 establishes the foundational compute environment for the wider Identity and Access Management learning path.

By recovering legacy hardware, configuring MX Linux, and preparing a baseline security toolkit, the project demonstrates the importance of a stable and appropriately configured environment for practical security learning.

The lab provides a starting point for subsequent exercises focused on cloud identity security, Microsoft Entra ID, authentication, RBAC, and identity operations.

---

**Lab status:** Foundational environment established.

**Next step:** Lab 1.2 — Minimal Cloud Identity Security Lab.
