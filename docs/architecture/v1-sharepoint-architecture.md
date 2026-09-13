# Enterprise Operations Hub — V1 SharePoint Architecture

## 1. Purpose

This document defines the initial technical architecture for Version 1 of the Enterprise Operations Hub.

V1 will implement a working:

**SharePoint Access / Permission Change Request**

The architecture intentionally begins with a small number of Microsoft technologies so the complete request lifecycle can be built, understood, tested, and documented before additional complexity is introduced.

---

# 2. V1 Architecture

The initial architecture is:

```text
Employee
    ↓
SharePoint Online
Enterprise Operations Hub
    ↓
Power Apps Request Form
    ↓
SharePoint Request List
    ↓
Power Automate
    ↓
Authorized Approver
    ↓
Approved / Rejected
    ↓
IT / M365 Administrator
    ↓
Manual Fulfillment
    ↓
Request Completed
```

V1 will use:

- SharePoint Online
- SharePoint Lists
- Power Apps
- Power Automate
- Microsoft 365 organizational identities

---

# 3. SharePoint Site

A dedicated SharePoint site will be created for the:

**Enterprise Operations Hub**

The site will function as the central employee-facing portal for the solution.

The portal will eventually provide navigation to areas such as:

- Home
- Submit Request
- My Requests
- Knowledge Base
- Policies
- Reports
- Administration

Not every section must be fully implemented during V1.

The primary V1 objective is the request-management process.

---

# 4. Initial SharePoint Site Type

The Enterprise Operations Hub will initially be designed as a modern SharePoint communication-style portal.

The portal is intended to provide information and services to a broad employee audience while administrative capabilities remain restricted.

Collaboration requirements will be evaluated separately rather than automatically granting broad editing permissions to portal users.

---

# 5. V1 Request Data

The primary V1 data store will be a SharePoint list.

Proposed list name:

```text
Access Requests
```

The list will store each SharePoint access or permission-change request as an individual record.

In ticketing-system terminology:

```text
One SharePoint list item = One request / ticket
```

Example:

```text
Request ID: AR-00001
Requester: John Smith
Request Type: New Access
Target Resource: Finance SharePoint Site
Requested Permission: Read
Business Justification: Quarterly reporting responsibilities
Status: Pending Approval
```

---

# 6. Why SharePoint List First?

V1 will use a SharePoint list rather than immediately introducing Dataverse.

Reasons include:

- SharePoint is already part of the Microsoft 365 environment.
- The initial data model is relatively simple.
- SharePoint lists integrate directly with Power Apps.
- SharePoint lists integrate directly with Power Automate.
- The architecture is sufficient for the initial proof of concept.
- It keeps V1 understandable and maintainable.

Dataverse can be evaluated later if the data model, security requirements, relationships, or application complexity justify migration.

---

# 7. Proposed Access Requests List

The initial list design will support information such as:

| Field                  | Purpose                              |
| ---------------------- | ------------------------------------ |
| Request ID             | Human-readable request identifier    |
| Requester              | User submitting the request          |
| Target User            | User whose access will change        |
| Request Type           | New, Change, or Remove access        |
| SharePoint Resource    | Resource requiring the access change |
| Requested Permission   | Requested standard permission level  |
| Business Justification | Reason access is required            |
| Additional Comments    | Optional requester information       |
| Status                 | Current request lifecycle status     |
| Approver               | Person responsible for approval      |
| Approval Decision      | Approved or Rejected                 |
| Approval Comments      | Approver explanation or comments     |
| Approval Date          | Date approval decision occurred      |
| Assigned Administrator | Administrator fulfilling the request |
| Fulfillment Notes      | Technical fulfillment information    |
| Completed Date         | Date fulfillment was completed       |

This is the initial logical design.

Exact SharePoint column names and data types will be defined before the list is created.

---

# 8. Permission Model

The solution will follow the principle of:

**Least Privilege**

Users should receive only the permissions required to perform their responsibilities.

Standard access requests will focus on permission levels such as:

- Read
- Contribute
- Edit where specifically justified

**Owner / Full Control will not be available through the standard employee request workflow.**

Elevated administrative access will eventually require a separate privileged-access process.

---

# 9. Group-Based Access

Where practical, SharePoint access should be granted through approved groups rather than directly to individual users.

Conceptual model:

```text
Employee
    ↓
Approved Group Membership
    ↓
SharePoint Permission
    ↓
SharePoint Resource
```

This provides a cleaner foundation for:

- Permission management
- Auditing
- User lifecycle management
- Automation
- Access reviews
- Identity governance

V1 may use manual fulfillment while preserving this architectural direction.

---

# 10. Power Apps Role

Power Apps will provide the employee-facing request form.

The application should make request submission easier and more controlled than directly editing the underlying SharePoint list.

The Power Apps interface will eventually:

- Identify the authenticated user
- Capture request information
- Validate required fields
- Restrict available permission choices
- Submit the request
- Display confirmation
- Support request tracking

Users should not require direct administrative access to the underlying request-management structure.

---

# 11. Power Automate Role

Power Automate will orchestrate the request workflow after submission.

Conceptual workflow:

```text
Request Submitted
        ↓
Validate Request
        ↓
Set Status = Pending Approval
        ↓
Send Approval
        ↓
     Decision
      /     \
 Approved   Rejected
    ↓          ↓
Update       Update
Status       Status
    ↓          ↓
Notify       Notify
Requester    Requester
    ↓
Assign for Fulfillment
    ↓
Administrator Performs Change
    ↓
Request Marked Completed
    ↓
Requester Notified
```

---

# 12. Approval vs. Fulfillment

Approval and fulfillment will remain separate stages.

## Approval

Approval answers:

> Should this person be authorized to receive this access?

## Fulfillment

Fulfillment answers:

> Has the approved technical change actually been performed?

For V1, fulfillment may be performed manually by an administrator.

This separation creates a future integration point for:

- Microsoft Graph
- PowerShell
- PnP PowerShell
- Entra group automation

---

# 13. Request Status Model

The planned lifecycle is:

```text
Draft
  ↓
Submitted
  ↓
Pending Approval
  ↓
Approved ──────────→ Rejected
  ↓
In Progress
  ↓
Completed
```

A request may also become:

```text
Cancelled
```

where appropriate.

Status transitions should be controlled by the workflow rather than allowing every user to freely change request status.

---

# 14. Basic User Roles

V1 will conceptually include the following roles.

## Requester

Can:

- Submit a request
- Provide business justification
- View their own requests
- View request status

Should not be able to:

- Approve their own request
- Modify approval records
- Mark requests completed
- Grant themselves permissions

## Approver

Can:

- Review assigned requests
- Approve requests
- Reject requests
- Provide approval comments

## IT / M365 Administrator

Can:

- Review approved requests
- Perform fulfillment
- Record fulfillment notes
- Mark fulfilled requests completed
- Troubleshoot the process

## Portal Administrator

Responsible for maintaining the Enterprise Operations Hub configuration.

Administrative access should be restricted.

---

# 15. Separation of Duties

Where practical, the architecture should prevent a requester from controlling the entire access lifecycle.

Conceptually:

```text
Requester
   ↓
Requests Access

Approver
   ↓
Authorizes Access

Administrator
   ↓
Implements Access
```

This provides stronger accountability than allowing one person to request, approve, and provision their own access.

V1 may simplify some role assignments because the environment is a development tenant, but the enterprise architecture will preserve this separation conceptually and document any testing exceptions.

---

# 16. Audit Trail

The system should preserve enough information to reconstruct the lifecycle of a request.

The audit trail should answer:

- Who submitted the request?
- Who needs access?
- What resource was requested?
- What permission was requested?
- Why was it requested?
- When was it submitted?
- Who reviewed it?
- What decision was made?
- When was the decision made?
- Who fulfilled it?
- When was fulfillment completed?

Future versions may introduce more advanced audit logging and reporting.

---

# 17. Initial Portal Structure

The planned portal navigation is:

```text
Enterprise Operations Hub
│
├── Home
├── Submit Request
├── My Requests
├── Knowledge Base
├── Policies
├── Reports
└── Administration
```

For V1, development will prioritize:

```text
Home
Submit Request
My Requests
Administration
```

Knowledge Base, Policies, and Reports can be expanded in later phases.

---

# 18. Security Boundary

Employees should interact primarily with the application and portal experience rather than directly managing the underlying request data.

Administrative fields should be protected from normal users.

Examples include:

- Approval Decision
- Approver
- Approval Date
- Assigned Administrator
- Fulfillment Notes
- Completed Date
- Workflow-controlled Status

The exact SharePoint and Power Apps security configuration will be determined during implementation and tested before being considered complete.

---

# 19. Future Architecture

After the V1 workflow is functional, the architecture may expand toward:

```text
Employee
    ↓
SharePoint Portal
    ↓
Power Apps
    ↓
SharePoint / Dataverse
    ↓
Power Automate
    ↓
Approval / Governance
    ↓
Microsoft Graph / PowerShell
    ↓
Microsoft Entra ID
    ↓
M365 / SharePoint Resources
    ↓
Audit / Reporting
    ↓
Power BI
```

Later governance capabilities may include:

- Access reviews
- Privileged-access workflows
- Automated provisioning
- Automated revocation
- Permission audits
- Identity lifecycle automation
- Security control mapping
- Governance reporting

---

# 20. V1 Architecture Principle

The guiding V1 principle is:

> Build a small, complete, secure, understandable workflow before building a large, incomplete platform.

The V1 architecture should demonstrate the complete lifecycle:

```text
Request
    ↓
Approval
    ↓
Fulfillment
    ↓
Verification
    ↓
Completion
    ↓
Audit Trail
```

Once this lifecycle works reliably, additional Microsoft technologies can be introduced to automate and strengthen individual stages.
