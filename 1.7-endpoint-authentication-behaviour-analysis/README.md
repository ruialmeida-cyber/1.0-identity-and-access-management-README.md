# 1.7 — Windows 11 Identity Telemetry Analysis Lab

## Endpoint Authentication & Access Behaviour Investigation

**Section:** 1.0 — Identity and Access Management
**Lab:** 1.7 — Endpoint Authentication Behaviour Analysis
**Platform:** Windows 11
**Primary data source:** Windows Security Event Logs
**Collection methods:** Event Viewer and PowerShell
**Related areas:** Endpoint identity telemetry, authentication monitoring, privilege analysis, and Microsoft Entra ID

---

## Overview

This repository documents an identity-focused security investigation conducted on a Windows 11 endpoint.

The investigation examines how authentication, privilege assignment, process creation, and session lifecycle events are represented in Windows Security audit logs.

The objective is to interpret identity behaviour as observable telemetry and establish a structured baseline of authentication and access patterns before attempting anomaly detection.

This work forms part of a broader progression towards identity-centric security monitoring and Microsoft Entra ID analysis.

---

## Investigation Scope

The analysis focuses on Windows Security Event Logs as a source of endpoint identity telemetry.

The primary goal is to understand how identity-related activity is recorded at endpoint level and how those records can support security investigations.

The investigation considers:

* Successful authentication.
* Failed authentication.
* Privileged session context.
* Process creation.
* Session termination.
* Behaviour across multiple observation windows.

The findings provide an endpoint-level perspective that can later be compared with cloud identity telemetry.

---

## Identity Telemetry Model

The original investigation used the following Windows Security Event IDs as its core identity signal set.

| Event ID | Event category                             | Investigative purpose                        |
| -------- | ------------------------------------------ | -------------------------------------------- |
| 4624     | Successful logon                           | Examine successful authentication activity   |
| 4625     | Failed logon                               | Examine unsuccessful authentication attempts |
| 4672     | Special privileges assigned to a new logon | Examine privileged logon contexts            |
| 4688     | Process creation                           | Examine process activity recorded by Windows |
| 4634     | Logoff                                     | Examine session termination activity         |

These events provide different perspectives on endpoint identity behaviour.

They should not be treated as a complete representation of the identity lifecycle in every environment. Their availability and interpretation depend on audit policy, event details, log retention, and the type of activity recorded.

In particular, Event ID 4672 indicates that special privileges were assigned to a new logon. It does not, by itself, prove that a user performed a privilege escalation during the observed session.

---

## Data Collection Methodology

The original investigation identifies the following collection methods:

* Windows Event Viewer filtering.
* PowerShell-based log querying.
* Time-windowed analysis.

Three observation windows were used.

| Observation window | Intended purpose                      |
| ------------------ | ------------------------------------- |
| 24 hours           | Short-term behavioural snapshot       |
| 7 days             | Operational stability analysis        |
| 30 days            | Longer-term identity behaviour trends |

A structured PowerShell script was used to extract event counts across these timeframes.

The purpose of using consistent observation windows was to support repeatability and comparison between short-term activity and longer-term patterns.

### Reproducibility considerations

For a repeatable analysis, record:

* The collection start and end times.
* The event IDs included.
* The Windows host being investigated.
* The PowerShell commands or script version used.
* The number of records returned for each event ID.
* Any errors, permissions limitations, or gaps in log availability.

The original investigation describes the collection approach, but the detailed script output has not been independently verified as part of this README.

---

## Behavioural Analysis Approach

The investigation treats identity not simply as a static configuration, but as a sequence of observable system behaviours.

The events are interpreted as follows:

* **Authentication events:** Signals associated with successful and unsuccessful logon activity.
* **Privilege assignment events:** Evidence of special privileges associated with a logon session.
* **Process creation events:** Records of process activity that may help provide context for identity-driven system interaction.
* **Session termination events:** Records that help investigate the end of a logon session.

Together, these signals can help analysts examine the relationship between authentication, session context, and subsequent endpoint activity.

This approach provides a foundation for comparing endpoint telemetry with identity-monitoring concepts used in Microsoft Entra ID and other cloud identity environments.

---

## Key Observations

The original investigation recorded the following findings across the observation windows.

### 1. Successful authentication was the dominant signal

Authentication success events were reported as the dominant event category.

This provides a baseline observation about the relative volume of successful authentication activity in the collected dataset.

The observation does not independently establish that all authentication activity was legitimate.

### 2. Authentication failures were relatively infrequent

The original notes report a low frequency of failed authentication events relative to successful events.

This is a useful baseline measure, but a low failure count does not, by itself, rule out password spraying, brute-force activity, or other authentication attacks.

Such conclusions require analysis of event details, source information, account distribution, timing, and the completeness of the collected logs.

### 3. Privileged session events were associated with successful authentication activity

The original notes describe a consistent relationship between successful authentication events and privileged session assignment events.

Event sequencing and correlation are necessary to establish the relationship between specific logon sessions and privilege-related events.

The presence of Event ID 4672 should be interpreted in the context of the account, logon identifier, assigned privileges, and expected system behaviour.

### 4. Process creation activity was reported as stable

The original analysis describes process creation events as stable, without observed burst-based anomalies.

This is a reported finding from the original investigation. Confirming it requires the underlying event counts, time distribution, process details, and applicable baseline.

### 5. Session lifecycle activity was observed

The original notes report a relatively small volume of session termination events compared with authentication activity.

This may reflect differences in event semantics, session behaviour, collection scope, or the way activity was counted.

Event ID 4634 should not automatically be interpreted as evidence that every related session has been fully closed across all applications or services.

---

## Cloud Identity Mapping

Endpoint identity telemetry can be conceptually compared with cloud identity monitoring.

| Windows endpoint telemetry                  | Related cloud identity concept                | Important distinction                                                              |
| ------------------------------------------- | --------------------------------------------- | ---------------------------------------------------------------------------------- |
| Event ID 4624 — successful logon            | Successful cloud sign-in                      | Windows logon and cloud sign-in are different events and require separate evidence |
| Event ID 4625 — failed logon                | Failed cloud sign-in                          | Failure reasons and authentication mechanisms differ by platform                   |
| Event ID 4672 — special privileges assigned | Privileged access context                     | This is not equivalent to a specific Microsoft Entra role activation               |
| Event ID 4688 — process creation            | Identity-related workload or process activity | Process creation is endpoint telemetry, not a cloud sign-in event                  |
| Event ID 4634 — logoff                      | Session lifecycle activity                    | Windows logoff and cloud session termination are not interchangeable               |

This mapping supports cross-domain interpretation, but it does not establish a direct one-to-one relationship between Windows events and Microsoft Entra ID events.

A genuine cross-platform investigation would need to correlate appropriate records using available timestamps, identities, host information, and other relevant identifiers.

---

## SOC and IAM Interpretation

From an Identity and Access Management perspective, the original investigation interpreted the collected telemetry as reflecting stable authentication behaviour, with no observed anomalous clustering or abnormal access patterns.

The original notes also reported a consistent relationship between authentication success and privileged session events across the observation windows.

Low authentication-failure frequency was interpreted as consistent with stable credential usage.

These are baseline interpretations, not proof that the endpoint was free of compromise or suspicious activity.

A more complete assessment would also consider:

* Which accounts generated the events.
* Whether the logon types were expected.
* The source addresses and authentication context, where available.
* The privileges associated with the logon sessions.
* The processes created after authentication.
* The timing and distribution of failed authentication attempts.
* Whether relevant audit events were missing or excluded.
* Whether the observed activity matched an established baseline for that endpoint.

---

## Technical Competencies Demonstrated

This investigation demonstrates work in the following areas:

* Windows Security Event Log interpretation.
* Identity behaviour analysis.
* Structured telemetry collection using PowerShell.
* Comparison of authentication activity across observation windows.
* Examination of privilege-related events.
* Analysis of process creation and session lifecycle telemetry.
* Baseline modelling for endpoint identity activity.
* Mapping endpoint identity concepts to cloud identity monitoring.

These competencies provide a foundation for further work in endpoint security monitoring, IAM operations, and identity-centric security investigations.

---

## Cloud Security Relevance

Endpoint identity telemetry can complement cloud identity investigations.

Understanding Windows authentication and privilege-related events helps analysts interpret identity activity on systems that may participate in hybrid environments.

This lab provides a starting point for later correlation with:

* Microsoft Entra ID sign-in logs.
* Microsoft Entra ID audit logs.
* Identity lifecycle operations.
* Role-based access control.
* Cloud authentication and access telemetry.

The relationship between endpoint and cloud events must be established through actual correlated records rather than assumed from conceptual similarity alone.

---

## Evidence and Reproducibility

The source repository listing supplied for this lab contains a `README.md` file. It does not list a separate evidence directory or supporting data files.

The original README describes PowerShell-based event extraction and observations across 24-hour, 7-day, and 30-day windows. However, the underlying script, event exports, and numerical counts were not included in the supplied repository listing.

For a stronger evidence-backed portfolio entry, preserve the actual outputs used in the investigation, where available.

Potential supporting evidence includes:

* The PowerShell collection script.
* Sanitised event-count summaries for each observation window.
* Exported Windows Security event records.
* Screenshots showing the filtering process in Event Viewer.
* A summary of the collection period and event IDs.
* Notes explaining how the observations were derived.

Do not create substitute results or claim that evidence exists if it has not been preserved.

Before publishing supporting files, remove credentials, access tokens, and unnecessary personal or system-identifying information.

---

## Outcome

This lab establishes a structured approach to examining identity behaviour on a Windows 11 endpoint using Windows Security Event Logs.

It covers authentication success and failure, privilege-related logon context, process creation, and session termination.

The original investigation reports a baseline dominated by successful authentication events, relatively low failure frequency, stable process activity, and no observed anomalous clustering in the examined windows.

These findings should be understood within the scope and limitations of the original dataset.

The work provides a foundation for more advanced endpoint identity monitoring and future correlation with Microsoft Entra ID telemetry.

---

## Portfolio Value Statement

This project demonstrates practical work with Windows Security Event Logs to examine authentication, privilege-related session context, process creation, and session lifecycle activity.

It shows how endpoint telemetry can be organised into a repeatable investigation and interpreted using Identity and Access Management concepts.

The lab also establishes a foundation for further work in identity monitoring, authentication analysis, access-control interpretation, and correlation between endpoint and cloud identity systems.

---

**Section:** 1.0 — Identity and Access Management
**Lab:** 1.7 — Endpoint Authentication Behaviour Analysis
**Platform:** Windows 11
**Primary data source:** Windows Security Event Logs
**Collection methods:** Event Viewer and PowerShell
**Related topics:** Endpoint identity telemetry, authentication monitoring, privilege analysis, session lifecycle, and Microsoft Entra ID
