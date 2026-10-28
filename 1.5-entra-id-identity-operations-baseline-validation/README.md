# 1.5 — Microsoft Entra ID Identity Operations

## Baseline Validation and Access State Analysis

**Section:** 1.0 — Identity and Access Management
**Lab:** 1.5 — Entra ID Identity Operations Baseline Validation
**Platform:** Microsoft Entra ID and Microsoft Graph API

---

## 1. Overview

This investigation examines identity state in Microsoft Entra ID using Microsoft Graph API and compares the current state with historical, event-driven identity drift analysis documented in an earlier lab.

The focus is on identity validation, role-based access control (RBAC), group-based access, and reconciliation between event-based and state-based identity models.

The investigation considers how current identity information can be used alongside historical audit events to develop a more complete understanding of identity operations.

---

## 2. Objectives

This lab addresses four core Identity and Access Management questions:

* What is the current identity state in Microsoft Entra ID?
* How does RBAC affect visibility of identity objects?
* Does group membership provide evidence of stable or changing access?
* How does the current identity state compare with historical identity drift findings?

The objective is to establish a repeatable method for validating identity state and interpreting access-related information.

---

## 3. Data Sources

The original investigation identifies the following data sources:

| Data source                        | Investigative purpose                                    |
| ---------------------------------- | -------------------------------------------------------- |
| Microsoft Graph API responses      | Examine identity and directory information               |
| Microsoft Entra ID tenant metadata | Establish the identity environment under investigation   |
| Group membership responses         | Review available group membership information            |
| RBAC-restricted responses          | Examine permission boundaries and directory visibility   |
| Historical audit-log analysis      | Provide context for previously recorded identity changes |

The findings depend on the information available to the authenticated identity and the permissions granted to it.

---

## 4. Methodology

The investigation follows a structured identity validation process:

1. Define the identity scope.
2. Validate the tenant using the Microsoft Graph organisation endpoint.
3. Retrieve the authenticated identity using the `/me` endpoint.
4. Examine group membership using `/me/memberOf`.
5. Test directory-role visibility using `/directoryRoles`.
6. Reconstruct the available current identity state.
7. Compare the current state with historical audit-log findings.

This approach combines state-based inspection with event-based investigation.

**Important distinction:** A current-state query describes information available at the time of collection. Historical audit records provide information about recorded events over time. Neither source should automatically be treated as a complete substitute for the other.

---

## 5. Identity Scope Definition

The original lab notes identify the following investigation scope.

### Primary identity

`iam-lab-user-01@ruialmeidadacunhagmail.onmicrosoft.com`

### Administrative actor referenced in the historical investigation

`rui.almeidadacunha_gmail.com#EXT#@ruialmeidadacunhagmail.onmicrosoft.com`

### Authentication context identity

`live.com#rui.almeidadacunha@gmail.com`

### Group under analysis

**Group name:** `IAM-Lab-Group`

**Group object ID:**

`0e7e5c30-9eff-467a-b1c1-44422b438c19`

These values are reproduced from the original notes to preserve the investigative context.

**Publication warning:** Review these identifiers and account references before publishing. Redact tenant-specific identifiers, personal identity information, and other details if they are not appropriate for public disclosure.

---

## 6. Tenant Validation

The original investigation used the Microsoft Graph organisation endpoint to examine the tenant context.

The recorded findings were:

* A single active Microsoft Entra ID tenant was reported.
* The directory was identified as the default directory configuration.
* A tenant ID was recorded.
* A verified domain was identified.

### Recorded tenant information

**Tenant ID:**

`2c0009ed-1f8d-41a1-9d6c-836d6fc700ab`

**Verified domain:**

`ruialmeidadacunhagmail.onmicrosoft.com`

### Interpretation

The original notes concluded that the identity scope was correctly established, with no cross-tenant ambiguity identified during the investigation.

This conclusion applies to the tenant information observed in that investigation. It should not be interpreted as proof that every possible cross-tenant relationship or configuration was examined.

---

## 7. Identity Validation

The `/me` endpoint was used to examine the authenticated identity.

The original investigation recorded the following observations:

* The authenticated Microsoft Entra ID identity was resolved.
* An object ID was available.
* The identity was associated with the expected tenant context.
* The authentication context was reported as consistent.

### Interpretation

The results were interpreted as indicating that the authenticated identity was resolved within the expected Microsoft Entra ID context.

The `/me` endpoint represents the identity associated with the current access token. The information returned depends on the token, the permissions available, and the applicable Microsoft Graph behaviour.

A complete identity assessment may require additional checks if the investigation needs to establish more than the identity represented by the current session.

---

## 8. Group Membership Analysis

The investigation used `/me/memberOf` to examine the authenticated identity's group and directory-object memberships.

The original notes recorded:

* At least one group membership was returned.
* A group object ID was visible.
* Some group metadata was partially restricted.
* The available information reflected the permissions of the authenticated identity.

### Interpretation

The results indicated that group membership information was available, while some directory details were not fully visible to the current identity.

Restricted visibility should be interpreted carefully. An access-denied response or partially populated result does not necessarily mean that an object or membership does not exist.

It may instead reflect the permissions and properties available to the requesting identity.

---

## 9. Role and Privilege Visibility

The original investigation reported that a query to `/directoryRoles` returned:

`Access Denied`

### Recorded interpretation

The original notes interpreted this response as evidence that directory-role enumeration was unavailable to the authenticated identity.

This is consistent with a permission boundary preventing that query from returning the requested information.

However, an access-denied response alone does not establish the complete privileged-role state of the tenant. It establishes that the request did not provide the requested role information under the conditions in which it was executed.

### Security relevance

Restricted directory visibility is important when evaluating identity permissions.

An investigation should distinguish between:

* An identity having no privileged role.
* An identity being unable to enumerate privileged roles.
* A request failing because of insufficient permissions or another access restriction.

These are different conditions and should not be treated as interchangeable.

---

## 10. Identity Drift Comparison

The original investigation compared current-state observations with historical identity drift findings.

### Historical event-based analysis

The earlier investigation recorded:

* A group membership removal event.
* A subsequent group membership re-addition event.
* An administrative actor associated with the changes.
* A reconstruction of identity changes using audit logs.

These observations represent the historical findings recorded in the original lab notes.

### Current state-based analysis

The current-state investigation recorded:

* The authenticated identity was resolved.
* Group membership information was available.
* Directory-role enumeration returned an access-denied response.
* The current state was interpreted as stable in the original notes.

### Comparison

| Investigation perspective | Purpose                                                                | Recorded observation                                                |
| ------------------------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------- |
| Historical audit events   | Examine recorded changes over time                                     | Group membership removal and re-addition were reported              |
| Current Graph API state   | Examine available identity information at collection time              | Identity and group membership information were returned             |
| RBAC visibility           | Examine the requesting identity's access to directory-role information | The `/directoryRoles` request returned access denied                |
| Combined analysis         | Compare recorded historical changes with current observations          | Current-state findings were interpreted alongside historical events |

### Interpretation and limitation

The original notes concluded that the historical group membership changes were not reflected as active identity drift in the current state.

That conclusion should be treated as an interpretation of the observations available to the investigation, rather than a guarantee that no identity changes or access anomalies existed.

A reliable drift assessment requires sufficient historical coverage, an appropriate current-state baseline, and evidence that the relevant identities, groups, and assignments have been compared.

---

## 11. Identity Model Architecture

The investigation illustrates two complementary perspectives on identity.

### Event layer

Historical event analysis focuses on what happened over time.

Relevant information may include:

* Microsoft Entra ID audit logs.
* Group membership changes.
* Identity lifecycle events.
* The actor associated with a recorded operation.
* The timestamps and sequence of recorded changes.

This layer supports temporal reconstruction.

### State layer

Current-state analysis focuses on the identity information available at a particular point in time.

Relevant information may include:

* Microsoft Graph API responses.
* Current identity attributes.
* Available group membership information.
* Role assignments and directory objects visible to the requesting identity.
* Permission-related restrictions.

This layer supports point-in-time assessment.

### Combined model

Using both perspectives can help investigators distinguish historical changes from the current state.

However, the quality of the conclusion depends on the completeness of the available events, the accuracy of the baseline, and the scope of the state queries.

---

## 12. Security Observations

The original notes recorded the following observations:

* RBAC restrictions affected directory visibility.
* The authenticated identity could retrieve some identity information.
* The `/directoryRoles` request returned access denied.
* Historical group membership changes had been recorded in the earlier investigation.
* The current-state observations were interpreted as showing no active identity drift.
* No privilege escalation was identified in the original analysis.

These statements represent the findings recorded in the supplied lab material. They have not been independently revalidated against the live tenant.

### Operational considerations

When interpreting identity data, investigators should:

* Confirm which identity executed each query.
* Record the permissions and authentication context where relevant.
* Distinguish missing information from confirmed absence.
* Compare historical events with current state.
* Avoid treating a single access-denied response as proof of the complete privilege state.
* Document uncertainty and evidence limitations.

---

## 13. Detection Engineering Extension

The original lab proposes identifying repeated group membership changes as a potential indicator of identity instability.

Repeated additions and removals can be relevant to investigations involving:

* Misconfiguration.
* Frequent administrative changes.
* Unstable access arrangements.
* Identity governance gaps.
* Unexpected changes to group-based access.

Repeated changes are not necessarily malicious. They should be assessed against the operational context, the identity involved, the initiating actor, and the associated change records.

### Detection goal

Identify repeated group membership additions and removals that may warrant further investigation.

### Detection hypothesis

A pattern of repeated group membership changes may indicate access instability or an administrative process requiring review.

The hypothesis should be validated against actual event data before being used as a detection rule.

---

## 14. Microsoft Sentinel KQL Query

The original lab included the following Microsoft Sentinel KQL query as a detection-engineering extension.

The supplied query was incomplete, so the version below completes the aggregation and output for the stated detection objective.

```kusto
AuditLogs
| where OperationName in ("Add member to group", "Remove member from group")
| extend Actor = tostring(InitiatedBy.user.userPrincipalName)
| extend Target = tostring(TargetResources[0].userPrincipalName)
| where isnotempty(Target)
| summarize
    ActionCount = count(),
    Actions = make_set(OperationName),
    FirstSeen = min(TimeGenerated),
    LastSeen = max(TimeGenerated)
    by Target, Actor
| where ActionCount > 1
| order by ActionCount desc
```

### Query purpose

The query:

1. Filters audit records for group membership additions and removals.
2. Extracts the initiating user's principal name where available.
3. Extracts a target principal name from the first target resource.
4. Groups records by target and actor.
5. Counts matching actions and records the first and last observed timestamps.
6. Returns groups with more than one matching action.

### Important limitations

* The query assumes that the relevant target principal name is available in `TargetResources[0].userPrincipalName`.
* Group membership events may identify the affected object through a different field or resource representation.
* The initiating actor may be an application or service principal rather than a user.
* A count greater than one does not, by itself, prove repeated add/remove cycles for the same group.
* A production detection should extract the group identifier and target object identifier from the actual event schema, then correlate additions and removals by identity, group, actor, and time window.

The query is a starting point for investigation, not proof that a detection has been deployed or validated.

---

## 15. Evidence and Reproducibility

The original standalone repository contains an `Evidence` directory.

The evidence should be preserved alongside the investigation wherever possible, particularly when it contains command outputs or other records that support the documented findings.

### Useful evidence types

* Microsoft Graph API request and response details.
* PowerShell output showing the commands executed and results returned.
* Tenant and identity validation output.
* Group membership query results.
* The `/directoryRoles` access-denied response.
* Relevant historical audit-log records.
* Notes documenting the comparison between historical events and current state.

### Evidence handling principles

* Preserve original evidence files.
* Record collection dates and relevant command details.
* Redact credentials, tokens, and sensitive personal information.
* Distinguish direct observations from interpretations.
* Do not claim that a query succeeded when it returned an error.
* Do not claim that a condition is absent merely because the requesting identity cannot see it.

**Evidence limitation:** This README is based on the supplied original lab notes. The actual files in the `Evidence` directory have not been independently inspected here.

---

## 16. Key Learning Outcomes

This lab supports the development of the following skills:

* Validating an authenticated identity using Microsoft Graph.
* Establishing the tenant context for an investigation.
* Reviewing group membership information.
* Understanding how permissions affect directory visibility.
* Interpreting access-denied responses.
* Comparing historical audit events with current identity state.
* Identifying the limitations of event-based and state-based analysis.
* Developing preliminary detection logic for repeated group membership changes.
* Documenting findings in a structured and reproducible format.

---

## 17. Conclusion

This lab examines Microsoft Entra ID identity operations through a combination of current-state queries and historical identity drift analysis.

The original findings describe an identity that could be resolved through Microsoft Graph, available group membership information, and restricted visibility of directory roles. Historical notes also recorded group membership changes that were compared with the current state.

The investigation demonstrates the value of combining event-based and state-based perspectives when reviewing identity behaviour.

Reliable conclusions depend on appropriate query scope, sufficient permissions, complete evidence, and careful interpretation of missing or restricted information.

---

**Section:** 1.0 — Identity and Access Management
**Lab:** 1.5 — Entra ID Identity Operations Baseline Validation
**Primary platform:** Microsoft Entra ID
**Investigation interface:** Microsoft Graph API
**Related areas:** Identity validation, group membership, RBAC, audit analysis, identity drift, and detection engineering
