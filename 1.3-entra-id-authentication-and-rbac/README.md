# 1.3 — Microsoft Entra ID Authentication and RBAC Analysis

**Section:** 1.0 — Identity and Access Management
**Lab:** 1.3 — Entra ID Authentication and Role-Based Access Control
**Date:** March 2026
**Platform:** Microsoft Entra ID

---

## 1. Overview

This lab explores Identity and Access Management (IAM) concepts within Microsoft Entra ID, focusing on the relationship between authentication, authorisation, and Role-Based Access Control (RBAC).

The objective is to understand how an identity is verified, how permissions are assigned, and how access decisions are governed within an enterprise identity environment.

The lab also considers the relationship between identity lifecycle events, audit records, and sign-in information as sources of evidence for IAM analysis.

This work contributes to the development of practical skills in identity investigation, access control interpretation, and cloud security operations.

---

## 2. Objectives

The main objectives of this lab are to:

* Distinguish authentication from authorisation.
* Understand the purpose of Microsoft Entra ID in cloud identity management.
* Examine the principles of Role-Based Access Control.
* Understand how roles and assignments influence access.
* Recognise the importance of scope and least privilege.
* Interpret identity lifecycle and authentication evidence.
* Develop a structured approach to documenting IAM findings.

---

## 3. Authentication and Authorisation

Authentication and authorisation are related but distinct security processes.

### Authentication — Who are you?

Authentication establishes whether an identity can be verified through an accepted authentication process.

Within Microsoft Entra ID, authentication-related information can help investigators understand sign-in activity and the outcome of authentication attempts.

Relevant areas include:

* Identity verification.
* Sign-in activity.
* Authentication outcomes.
* Sign-in failures and their possible causes.
* Authentication-related events and records.

### Authorisation — What are you allowed to do?

Authorisation determines which actions an authenticated identity is permitted to perform on a resource.

Access decisions depend on the relevant permissions, role assignments, resource scope, and applicable security controls.

Relevant areas include:

* Role assignments.
* Permissions and privileges.
* Resource scope.
* Access governance.
* Least-privilege principles.

**Key distinction:** Successful authentication does not automatically mean that an identity has permission to access every resource.

---

## 4. Role-Based Access Control (RBAC)

Role-Based Access Control is an authorisation model in which permissions are associated with roles and access is granted through appropriate role assignments.

RBAC helps organisations manage access consistently rather than assigning every permission independently to every identity.

### Core components

| Component       | Purpose                                                                                    |
| --------------- | ------------------------------------------------------------------------------------------ |
| Identity        | The user, group, service principal, or other supported security principal receiving access |
| Role definition | Specifies the permissions available through a role                                         |
| Role assignment | Associates a role with a security principal at a defined scope                             |
| Scope           | Defines the resources or management boundary to which the assignment applies               |
| Permissions     | Determine the actions that can be performed                                                |
| Governance      | Supports appropriate access, accountability, and review                                    |

The precise meaning of a role depends on the platform and role type.

For example, Microsoft Entra ID directory roles govern directory-level administrative permissions, while Azure RBAC roles govern access to Azure resources.

These are related but distinct authorisation systems.

---

## 5. Microsoft Entra ID and Azure RBAC

Understanding the distinction between Microsoft Entra ID directory roles and Azure RBAC is important when analysing access.

### Microsoft Entra ID directory roles

Directory roles control administrative permissions within Microsoft Entra ID and related identity services.

Depending on the role, these permissions may include managing users, groups, applications, or other directory objects.

### Azure RBAC roles

Azure RBAC controls access to Azure resources.

Assignments can apply at different scopes, including:

* Management group.
* Subscription.
* Resource group.
* Individual resource.

An assignment at a broader scope may apply to resources beneath that scope, subject to the relevant authorisation model and applicable conditions.

### Why the distinction matters

A person may have permission to administer certain directory objects without having permission to manage a particular Azure resource.

Conversely, an Azure resource role does not automatically grant unrestricted administrative control over Microsoft Entra ID.

Investigations must therefore identify the relevant platform, role type, assignment, and scope before drawing conclusions about access.

---

## 6. Least Privilege and Access Governance

The principle of least privilege states that identities should receive only the permissions required to perform their authorised responsibilities.

Excessive permissions can increase the impact of compromised accounts, accidental changes, and misuse of administrative access.

A structured IAM review should consider:

* Whether an assignment is necessary.
* Whether the role grants more permissions than required.
* Whether the assignment scope is appropriate.
* Whether administrative access is adequately controlled.
* Whether access should be reviewed or removed.
* Whether available evidence supports the conclusions.

Least privilege is not demonstrated merely by identifying a role. It requires understanding the permissions, context, scope, and operational requirements associated with that role.

---

## 7. Identity Lifecycle and Audit Evidence

Identity lifecycle events can influence access and security posture.

Changes to users, groups, role assignments, and other identity objects may be relevant when investigating unexpected access or administrative activity.

Audit and sign-in records provide different perspectives on identity activity.

| Evidence source                | Investigative value                                                                                               |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| Audit logs                     | Help identify recorded changes to directory objects and administrative configuration                              |
| Sign-in logs                   | Help investigate recorded authentication and sign-in activity                                                     |
| Role assignment information    | Helps establish which roles are assigned and at what scope                                                        |
| Identity and group information | Helps establish relevant identity attributes and group relationships                                              |
| Configuration information      | Helps establish the state of relevant controls at the time of examination, where historical evidence is available |

The availability and detail of records depend on configuration, permissions, licensing, retention, and the time of investigation.

A log entry should be interpreted in context. A recorded event may establish that an operation was logged, but it does not necessarily prove every resulting access consequence.

---

## 8. Evidence and Investigation Approach

This lab includes an `Evidence` directory in the original standalone repository.

The evidence associated with an investigation should support the findings being documented and should be handled carefully when preparing a public portfolio.

### Evidence handling principles

* Preserve original evidence where possible.
* Record the source and collection date.
* Distinguish observed results from interpretation.
* Avoid presenting assumptions as verified findings.
* Remove or redact sensitive tenant details, personal information, and credentials before publication.
* Do not publish access tokens, secrets, or other authentication material.
* Retain sufficient context for another person to understand what the evidence demonstrates.

Where PowerShell output is used, it can provide a readable record of the commands executed and the results returned.

For reproducibility, relevant documentation should identify the purpose of the command, the environment in which it was executed, and any limitations affecting the output.

**Evidence limitation:** The existence of an evidence directory does not, by itself, establish the content or completeness of its files. Findings should be based on the evidence actually available and reviewed.

---

## 9. Investigation Methodology

A consistent IAM investigation should follow a defined sequence.

### Step 1 — Establish the context

Identify the relevant identity platform, the investigation objective, and the scope of the activity being examined.

### Step 2 — Establish the available state

Identify the relevant identities, roles, assignments, or records available for examination.

### Step 3 — Examine the evidence

Review applicable audit records, sign-in information, role assignments, and configuration details.

### Step 4 — Interpret the results

Determine what the available information establishes and identify any gaps or uncertainties.

### Step 5 — Document the findings

Record the observed results, their security relevance, and any limitations.

### Step 6 — Identify follow-up actions

Where appropriate, identify additional evidence or validation required to confirm the conclusion.

This methodology promotes repeatability and helps separate technical observations from assumptions.

---

## 10. Security Relevance

Authentication and access control are fundamental components of enterprise security.

Weak access governance, excessive permissions, and insufficient monitoring can increase the risk of unauthorised activity and make investigations more difficult.

The concepts explored in this lab are relevant to:

* Identity and Access Management operations.
* Microsoft Entra ID administration and support.
* Access control reviews.
* Identity lifecycle investigations.
* Cloud security operations.
* Security monitoring and incident investigation.
* Least-privilege assessment.

The purpose is to develop an analytical understanding of identity systems rather than treating role assignment as an isolated administrative task.

---

## 11. Key Learning Outcomes

This lab supports the development of the following knowledge and skills:

* Understanding the difference between authentication and authorisation.
* Explaining the purpose of RBAC.
* Distinguishing Microsoft Entra ID directory roles from Azure RBAC roles.
* Understanding role assignments and scope.
* Applying least-privilege reasoning.
* Recognising the investigative value of audit and sign-in records.
* Documenting technical findings in a structured format.
* Identifying evidence limitations and avoiding unsupported conclusions.

---

## 12. Conclusion

This lab establishes a foundation for understanding Microsoft Entra ID authentication and role-based access control.

By examining the relationship between identity verification, authorisation, role assignments, and audit evidence, it provides a structured basis for further IAM investigation.

The central principle is that access must be understood in context: the identity involved, the permissions granted, the applicable scope, and the available evidence all contribute to an accurate assessment.

This lab forms part of the broader Identity and Access Management learning path and prepares for more focused work on role assignment validation and identity operations.

---

**Section:** 1.0 — Identity and Access Management
**Lab:** 1.3 — Entra ID Authentication and Role-Based Access Control
**Primary platform:** Microsoft Entra ID
**Related concepts:** Authentication, authorisation, RBAC, least privilege, identity lifecycle, audit evidence
