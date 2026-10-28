# 1.4 — Microsoft Entra ID Role Assignment Validation

**Section:** 1.0 — Identity and Access Management
**Lab:** 1.4 — Entra ID Role Assignment Validation
**Platform:** Microsoft Entra ID
**Focus:** Privileged access, role assignments, identity validation, and RBAC integrity

---

## 1. Overview

This lab documents the validation of a privileged role assignment in Microsoft Entra ID, focusing on the built-in **Global Administrator** directory role.

The investigation examines role assignment information, principal identity consistency, role definition identifiers, and directory scope.

It also investigates an apparent duplication in the Microsoft Entra admin centre interface, distinguishing repeated visual representations from independently confirmed role assignments.

The objective is to demonstrate a structured approach to privileged identity validation and to avoid drawing security conclusions based solely on how information is displayed in a portal.

---

## 2. Objectives

The objectives of this lab are to:

* Identify a Global Administrator role assignment.
* Examine the role definition and principal identifiers.
* Validate the relationship between the identity and the assigned role.
* Review the reported directory scope.
* Investigate apparent duplicate entries in the administrative interface.
* Distinguish observations from conclusions supported by available evidence.
* Understand the importance of validating privileged access accurately.

---

## 3. Environment and Scope

The investigation was performed through the Microsoft Entra admin centre.

The scope was limited to reviewing the Global Administrator directory role and the assignment information presented in the administrative interface.

### Role under investigation

| Attribute          | Observed value                         |
| ------------------ | -------------------------------------- |
| Role name          | Global Administrator                   |
| Role definition ID | `62e90394-69f5-4237-9190-012177145e10` |
| Principal ID       | `e725c212-4d94-4ae4-9bf1-62422d7bac76` |
| Reported scope     | Default Directory (Directory)          |

**Security note:** The identifiers above are retained from the original lab notes. Before publishing this README, ensure that the principal ID and any associated evidence are appropriate for public disclosure.

---

## 4. Procedure

### Step 1 — Access role management

The Microsoft Entra admin centre was opened, and the following navigation was used:

1. Open Microsoft Entra ID.
2. Navigate to **Roles and administrators**.
3. Select **Global Administrator**.
4. Review the available role assignment information.

### Step 2 — Review the assignment

The role assignment information was examined to identify the principal, role definition, and scope.

The recorded values were:

* **Principal ID:** `e725c212-4d94-4ae4-9bf1-62422d7bac76`
* **Role definition ID:** `62e90394-69f5-4237-9190-012177145e10`
* **Role:** Global Administrator
* **Scope:** Default Directory (Directory)

These attributes provide reference points for checking whether displayed entries refer to the same identity and role.

### Step 3 — Investigate the interface observation

Multiple entries appeared in the portal's role assignment view.

The original investigation notes reported that the entries appeared to share the same underlying identifiers.

This raised the question of whether the interface was displaying duplicate representations or whether multiple independent role assignments existed.

### Step 4 — Validate the recorded information

The available assignment information was compared across three attributes:

* Principal ID.
* Role definition ID.
* Directory scope.

The recorded findings indicated consistency across these attributes.

Matching identifiers support the interpretation that entries may refer to the same underlying assignment. However, a definitive determination that no separate assignments exist requires examination of the underlying assignment records, rather than relying on the portal display alone.

---

## 5. Findings

The original investigation recorded the following observations.

| Area                  | Finding                                                                            |
| --------------------- | ---------------------------------------------------------------------------------- |
| Privileged role       | Global Administrator was selected for review                                       |
| Principal identity    | A principal ID was recorded                                                        |
| Role definition       | The Global Administrator role definition ID was recorded                           |
| Scope                 | The assignment was reported at directory scope                                     |
| Portal display        | Multiple entries appeared in the interface                                         |
| Identifier comparison | The recorded identifiers were reported as consistent                               |
| Validation limitation | A definitive backend-level conclusion depends on the underlying assignment records |

### Interpretation

The observations illustrate why role assignment validation should use stable identifiers and assignment data rather than relying exclusively on visual presentation.

Repeated entries in an interface do not, by themselves, prove that duplicate privileged assignments exist.

Equally, matching identifiers in a screenshot or summary are not sufficient on their own to establish the complete state of the underlying authorisation system.

The appropriate conclusion must reflect the strength and completeness of the evidence actually examined.

---

## 6. Evidence

The original standalone repository contains the README and licence. The supplied repository listing does not show a separate evidence directory for this lab.

The original lab notes document the portal observations and the recorded identifiers.

Where available, supporting evidence can include:

* Screenshots of the Global Administrator role assignment view.
* PowerShell output showing relevant role definitions and assignments.
* Command output identifying the principal, role definition, and scope.
* Exported assignment records suitable for comparison.
* Notes documenting the validation procedure and observed results.

### Evidence handling

For reproducibility, evidence should include enough context to identify:

1. The command or interface used.
2. The information being examined.
3. The relevant identifiers and scope.
4. The observed output.
5. Any limitations affecting the conclusion.

PowerShell output can be useful because it provides a text-based record that can be reviewed alongside the documented procedure.

Sensitive identifiers and tenant information should be reviewed before any evidence is published publicly.

**Evidence limitation:** This README reflects the findings recorded in the supplied original notes. It does not independently verify the underlying tenant state or establish that additional backend queries were executed.

---

## 7. Security Significance

Global Administrator is a highly privileged Microsoft Entra ID directory role.

Assignments to this role warrant particular care because excessive or incorrectly assigned administrative permissions can significantly increase security risk.

Accurate validation supports:

* Privileged access reviews.
* Identity governance.
* Audit preparation.
* Investigation of unexpected administrative access.
* Least-privilege assessments.
* Reliable interpretation of identity data.

Misinterpreting a portal display can lead to either a false positive, where an investigator reports duplication that has not been established, or a false negative, where a genuine assignment issue is overlooked.

The investigation must therefore distinguish interface observations from confirmed authorisation data.

---

## 8. Key Concepts

### Principal ID

The principal ID identifies the security principal associated with a role assignment. Its meaning should be interpreted in the context of the relevant identity object and assignment record.

### Role definition ID

The role definition ID identifies the role definition being assigned. Comparing it helps establish which role an assignment references.

### Scope

Scope determines the boundary within which an assignment applies. The scope must be examined alongside the role and principal when evaluating access.

### Assignment versus display

A portal entry is a representation of information. Confirming the underlying assignment state requires appropriate examination of the actual assignment records.

### Evidence-based validation

Conclusions should be supported by the data collected during the investigation, with limitations clearly documented.

---

## 9. Outcome

The original lab notes report that the Global Administrator role assignment information was reviewed and that the principal ID, role definition ID, and directory scope appeared consistent across the displayed entries.

The investigation highlights the importance of validating privileged role assignments using relevant identifiers and underlying assignment data.

A definitive claim that only one assignment exists should be made only where the available evidence establishes that conclusion.

---

## 10. Conclusion

This lab demonstrates a structured approach to reviewing privileged role assignment information in Microsoft Entra ID.

The investigation focuses on the Global Administrator role and the use of principal ID, role definition ID, and scope when interpreting role assignment data.

The key lesson is that visual duplication should not automatically be treated as an underlying RBAC duplication. Equally, conclusions about the integrity of privileged access must be supported by appropriate evidence.

Reliable role assignment validation depends on examining the relevant identity, role, scope, and assignment records together.

---

## 11. Position in the Learning Path

This lab forms part of **Section 1.0 — Identity and Access Management**.

It follows Lab 1.3, which introduces Microsoft Entra ID authentication and RBAC concepts, and provides a practical focus on validating privileged role assignment information.

The next lab is:

**Lab 1.5 — Entra ID Identity Operations Baseline Validation**

That lab progresses towards establishing and reviewing an identity operations baseline.

---

**Section:** 1.0 — Identity and Access Management
**Lab:** 1.4 — Entra ID Role Assignment Validation
**Primary platform:** Microsoft Entra ID
**Core focus:** Privileged role assignments, identity identifiers, scope, and evidence-based validation
