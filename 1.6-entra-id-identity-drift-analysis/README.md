# 1.6 — Microsoft Entra ID Identity Drift & Access Evolution Analysis

**Section:** 1.0 — Identity and Access Management
**Lab:** 1.6 — Entra ID Identity Drift Analysis
**Platform:** Microsoft Entra ID
**Data source:** Entra ID audit logs
**Detection platform:** Microsoft Sentinel / KQL

---

## Overview

This investigation reconstructs identity behaviour in Microsoft Entra ID using exported audit logs.

The focus is on identity drift, group-based access evolution, and actor-driven identity changes.

Rather than treating audit logs as isolated records, this lab applies a correlation-first Security Operations Centre (SOC) methodology to reconstruct identity activity over time.

The investigation examines who performed identity changes, which identities were affected, when the changes occurred, and how group membership changes may influence access.

---

## Objectives

This lab addresses four core Identity and Access Management questions:

* Who performed identity changes?
* When did access changes occur?
* How did group membership influence effective permissions?
* Does the observed identity history indicate stable access or potential identity drift?

The objective is to develop a repeatable approach to reconstructing identity activity from audit records while recognising the limitations of event-based evidence.

---

## Dataset

The investigation uses the following evidence file:

```text
evidence/audit_logs.csv
```

The CSV file is intended to provide the audit events used for identity activity reconstruction.

The conclusions in this README reflect the original investigation notes. The contents of the CSV have not been independently revalidated here.

---

## Methodology

The investigation follows these stages:

1. Identity scope definition.
2. Actor and target mapping.
3. Event sequencing and timeline reconstruction.
4. Access-state inference.
5. Identity drift analysis.
6. Detection-engineering considerations.

The purpose is to connect individual audit events into an understandable sequence while distinguishing recorded activity from inferred access effects.

---

## 1. Identity Scope Definition

### Primary identity

`iam-lab-user-01@ruialmeidadacunhagmail.onmicrosoft.com`

### Administrative actor

`rui.almeidadacunha_gmail.com#EXT#@ruialmeidadacunhagmail.onmicrosoft.com`

### Authentication identity — non-control-plane activity

`live.com#rui.almeidadacunha@gmail.com`

### Group under analysis

**Group name:** `IAM-Lab-Group`

**Group object ID:**

`0e7e5c30-9eff-467a-b1c1-44422b438c19`

These identifiers are retained from the original investigation notes to preserve the technical context.

**Publication note:** Before publishing this README publicly, review tenant-specific identifiers, user principal names, external identity references, and evidence files. Redact information that should not be publicly disclosed.

---

## 2. Actor Mapping

### Control-plane actor

The original analysis attributes structural identity modifications to the following privileged actor:

`rui.almeidadacunha_gmail.com#EXT#@ruialmeidadacunhagmail.onmicrosoft.com`

The recorded capabilities associated with this actor include:

* Adding and removing group members.
* Modifying identity access assignments.
* Executing directory-level changes.

These capabilities are described in the original notes. They should not be interpreted as a complete inventory of the actor's effective permissions without supporting role-assignment evidence.

### Service-principal actor

**Actor:** `Azure MFA StrongAuthenticationService`

The original analysis associates this service with:

* Authentication-method updates.
* MFA configuration modifications.

Service-principal activity should be distinguished from activity initiated interactively by a human administrator. The exact operation and actor attribution should be confirmed against the corresponding audit records.

### Authentication identity

The original notes identify the following authentication identity:

`live.com#rui.almeidadacunha@gmail.com`

The recorded activity associated with this identity was limited to sign-in events, rather than directory control-plane modifications.

This distinction helps separate authentication activity from administrative changes to directory objects.

---

## 3. Timeline Reconstruction

The original investigation describes three events.

### Event 1 — Group removal

| Field              | Recorded observation                           |
| ------------------ | ---------------------------------------------- |
| Action             | Remove member from `IAM-Lab-Group`             |
| Actor              | Tenant administrator                           |
| Target             | `iam-lab-user-01`                              |
| Interpreted effect | Potential temporary loss of group-based access |

The removal event indicates that a group membership change was recorded.

The actual access impact depends on the permissions associated with the group and any other permissions or memberships available to the target identity.

### Event 2 — Group addition

| Field              | Recorded observation                            |
| ------------------ | ----------------------------------------------- |
| Action             | Add member to `IAM-Lab-Group`                   |
| Actor              | Tenant administrator                            |
| Target             | `iam-lab-user-01`                               |
| Interpreted effect | Restoration of access associated with the group |

The subsequent addition event indicates that group membership was changed again.

If the group provides access through an RBAC assignment, restoring membership may restore the access associated with that assignment. This effect should be confirmed against the group's actual permissions and the relevant assignment configuration.

### Event 3 — MFA update

| Field              | Recorded observation                                  |
| ------------------ | ----------------------------------------------------- |
| Action             | Authentication-method update                          |
| Actor              | Azure MFA service                                     |
| Target             | `iam-lab-user-01`                                     |
| Interpreted effect | Change to the identity's authentication configuration |

The original analysis records an authentication-method update associated with the target identity.

An authentication-method update can affect authentication posture, but its precise security impact depends on the operation performed and the resulting configuration.

### Timeline interpretation

Together, the three recorded events provide a basis for examining group membership changes and authentication-related activity affecting the same identity.

A full reconstruction should preserve the original event timestamps, operation names, actor identifiers, target identifiers, and relevant correlation information.

---

## 4. Access Drift Analysis

### Definition

Access drift refers to divergence between:

* Expected identity permissions.
* The observed or accumulated access state over time.

Drift may arise through group membership changes, role assignments, identity lifecycle operations, or other changes to access configuration.

Audit events can help explain how a state changed, but they do not necessarily provide a complete representation of current effective permissions.

### Key observation 1 — Group-based access can affect effective permissions

Group membership may grant access through group-based role assignments or other resource permissions.

Adding or removing a member can therefore change the access available to that identity.

However, membership changes do not necessarily accumulate permissions indefinitely. The result depends on the relevant group assignments, nested memberships, resource permissions, and other access paths.

### Key observation 2 — Audit logs are not a complete state model

Audit logs represent recorded events. They do not, on their own, establish every aspect of current effective access.

For example, a group removal event may explain why an access path changed, but it does not prove that all access was removed from the target identity.

A complete assessment may require current membership information, role assignments, resource permissions, and other relevant configuration data.

### Key observation 3 — Administrative actor attribution matters

The original analysis attributes the structural changes to a privileged administrative actor.

Actor attribution helps investigators determine which identity initiated a change and whether the action was expected.

The attribution should be supported by the relevant audit records, including the actor fields and operation details.

### Security insight

The original investigation highlights several important considerations:

* Group-based access can create dependencies that are not obvious from an individual identity's attributes.
* Identity state may need to be reconstructed by correlating events.
* Static assumptions about access can become outdated when memberships or assignments change.
* Privileged actor activity should be reviewed in context.
* Event history and current access state should be examined together.

These observations support further investigation; they do not independently establish malicious activity or privilege escalation.

---

## 5. Detection Engineering Extension — Microsoft Sentinel / KQL

### Detection goal

Identify repeated group membership additions and removals affecting the same target identity within a short period.

Potential explanations include:

* Configuration errors.
* Repeated administrative corrections.
* Unstable access arrangements.
* Suspicious access changes.
* Unexpected administrative activity.

Repeated changes are not necessarily malicious. Their significance depends on the target, group, actor, sequence, timing, and operational context.

### Detection hypothesis

A series of group membership additions and removals affecting the same identity may indicate access instability or an administrative process that warrants investigation.

### Microsoft Sentinel KQL query

The following query preserves the original investigation's one-hour grouping approach.

```kusto
AuditLogs
| where OperationName in (
    "Add member to group",
    "Remove member from group"
)
| extend Actor = tostring(InitiatedBy.user.userPrincipalName)
| extend Target = tostring(TargetResources[0].userPrincipalName)
| where isnotempty(Target)
| summarize
    ActionCount = count(),
    Actions = make_set(OperationName),
    FirstSeen = min(TimeGenerated),
    LastSeen = max(TimeGenerated)
    by Actor, Target, bin(TimeGenerated, 1h)
| where ActionCount > 1
| order by ActionCount desc
```

### Query explanation

The query:

1. Filters audit records for group membership addition and removal operations.
2. Extracts the initiating user's principal name where available.
3. Extracts the target principal name from the first target resource.
4. Groups events by actor, target, and one-hour time interval.
5. Counts matching actions and records the first and last observed timestamps.
6. Returns groups with more than one matching event.

### Limitations

The query is a starting point for detection engineering, not a validated production detection.

In particular:

* The target principal name may not be present in `TargetResources[0].userPrincipalName`.
* The target resource may represent a group or another directory object rather than a user.
* Automated activity may be initiated by an application or service principal instead of a user.
* Multiple events within one hour do not necessarily constitute a complete add/remove cycle.
* The query does not explicitly correlate events to a specific group object.
* A high event count does not prove malicious intent.

For stronger correlation, extend the query to extract the relevant target identity and group identifiers from the actual event schema. Correlate additions and removals by target, group, actor, and time window, then validate the results against known administrative activity.

---

## 6. Evidence and Reproducibility

The original standalone repository includes the following investigation materials:

```text
evidence/
IAM_analysis.md
LICENSE
README.md
```

The primary dataset is identified as:

```text
evidence/audit_logs.csv
```

### Evidence handling

For a reproducible investigation, preserve:

* The original audit-log export.
* The analysis notes.
* The query used to identify relevant events.
* The timestamps and actor/target fields supporting the timeline.
* Any additional outputs used to infer access effects.

Keep original evidence separate from derived analysis where possible.

Do not modify the original evidence simply to make it match the conclusions in the README. If an interpretation changes, document the change and its reasoning.

### Evidence limitations

The original notes describe the group removal, subsequent group addition, and MFA update. The evidence files have not been independently inspected here, so these are presented as the findings recorded by the original investigation rather than independently confirmed tenant activity.

---

## 7. Key Learning Outcomes

This lab develops practical understanding of:

* Identity activity reconstruction from audit logs.
* Mapping administrative actors to affected identities.
* Separating authentication events from directory control-plane activity.
* Analysing group membership changes.
* Understanding the difference between event history and current access state.
* Recognising the limitations of inferring effective permissions from audit events alone.
* Developing preliminary KQL detection logic.
* Documenting findings with appropriate evidence limitations.

---

## 8. Conclusion

This investigation examines identity drift and access evolution in Microsoft Entra ID by correlating audit events associated with group membership and authentication-method changes.

The original analysis describes a group membership removal, a subsequent addition, and an MFA-related update. These observations provide a basis for investigating identity changes over time and understanding how administrative activity may affect access.

The lab also demonstrates why audit events should not be treated as a complete model of current effective permissions. Reliable conclusions require appropriate actor attribution, event correlation, knowledge of the relevant access configuration, and supporting evidence.

The KQL query provides a preliminary method for identifying repeated group membership changes. Further validation is needed before using it as a production detection.

---

**Section:** 1.0 — Identity and Access Management
**Lab:** 1.6 — Entra ID Identity Drift Analysis
**Platform:** Microsoft Entra ID
**Data source:** Entra ID audit logs
**Detection platform:** Microsoft Sentinel / KQL
**Related topics:** Identity operations, group membership, RBAC, audit analysis, access evolution, and detection engineering
