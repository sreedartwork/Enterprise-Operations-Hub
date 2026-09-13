````markdown
# Enterprise Operations Hub — Environment Setup

## Purpose

This document records the development environment used to build the Enterprise Operations Hub.

The purpose of documenting the environment is to make the project reproducible and to provide a clear technical record of the Microsoft 365, SharePoint, Power Platform, identity, development, and source-control resources used during development.

This document distinguishes between:

- Technologies currently configured and verified
- Technologies available for development
- Technologies planned for future project phases

A technology will not be presented as an implemented portfolio skill until it has actually been configured, used, and tested within the project.

---

# 1. Project Environment Overview

The Enterprise Operations Hub is being developed as an enterprise-style Microsoft 365 operations and request-management solution.

The project environment is designed to support development and testing involving:

- Microsoft 365
- SharePoint Online
- Microsoft Entra ID
- Power Apps
- Power Automate
- Dataverse
- Power BI
- PowerShell
- PnP PowerShell
- Microsoft Graph
- Identity governance
- Security governance
- GRC concepts
- NIST Cybersecurity Framework
- CIS Controls
- Future C# / ASP.NET Core development
- Future Microsoft Azure integration

The project will be built incrementally rather than attempting to configure every technology at the beginning.

---

# 2. Microsoft 365 Organization

## Organization

**Organization Name:** Urban Assessory LLC

A dedicated Microsoft 365 organizational tenant was established for development of the Enterprise Operations Hub.

This provides a realistic Microsoft cloud environment rather than attempting to build the solution entirely with a personal Microsoft account.

---

# 3. Microsoft 365 Tenant

## Tenant Domain

The Microsoft 365 tenant uses the following organizational domain:

```text
<tenant>.onmicrosoft.com
```
````

The `.onmicrosoft.com` domain is the default organizational domain created by Microsoft when a Microsoft 365 tenant is established.

It provides the organization with its own Microsoft cloud identity environment.

---

# 4. Development / Administrative Account

The primary development and administrative account is:

```text
<admin-account>@<tenant>.onmicrosoft.com
```

This is a Microsoft organizational account rather than a personal Microsoft account.

The organizational account is used to access administrative and development services such as:

- Microsoft 365 Admin Center
- SharePoint Admin Center
- Microsoft Entra
- Power Apps
- Power Automate
- Power Platform
- Exchange
- Teams

## Why an Organizational Account Is Required

In plain English, the organizational account represents a user who belongs to the company's Microsoft environment.

A personal Microsoft account can access many Microsoft consumer services, but enterprise technologies such as SharePoint administration, organizational identity management, and many Power Platform capabilities require a work or school identity associated with a Microsoft tenant.

---

# 5. Microsoft 365 Subscription

The development tenant currently uses:

**Microsoft 365 Business Basic**

The subscription was selected to provide the Microsoft 365 cloud services required to build the initial version of the Enterprise Operations Hub.

The subscription currently provides access to services including:

- SharePoint Online
- Microsoft Teams
- Exchange Online
- OneDrive
- Microsoft 365 web applications
- Microsoft 365 organizational identity services

## Subscription Strategy

The project is being developed with cost control in mind.

The goal is to use free development resources whenever practical and only maintain paid services when they provide meaningful portfolio or development value.

The Microsoft 365 subscription provides the SharePoint Online tenant required for the project.

Additional Microsoft services will not be purchased simply to increase the number of technologies listed in the portfolio.

---

# 6. SharePoint Online

SharePoint Online has been successfully provisioned for the Microsoft 365 tenant.

The SharePoint Admin Center has been accessed successfully and active SharePoint sites were visible.

This confirms that SharePoint Online is operational within the development tenant.

## SharePoint Admin Center

```text
https://<tenant>-admin.sharepoint.com
```

## Role of SharePoint in the Project

SharePoint Online will provide the primary enterprise portal for the Enterprise Operations Hub.

Planned SharePoint responsibilities include:

- Portal pages
- Site navigation
- Request data
- SharePoint lists
- Document libraries
- Knowledge base content
- Policies
- Permissions
- Metadata
- Content types
- Search
- Information architecture
- Governance documentation
- Administrative resources

## Plain-English Explanation

SharePoint will essentially provide the project's internal company website and part of its data-management layer.

Employees will eventually be able to visit the Enterprise Operations Hub to submit requests, review information, locate policies, access knowledge resources, and view information appropriate to their role.

---

# 7. Microsoft Entra ID

Microsoft Entra ID is available as the identity system associated with the Microsoft 365 tenant.

## Plain-English Explanation

Microsoft Entra ID is Microsoft's cloud identity and access-management system.

It determines things such as:

- Who a user is
- Whether the user can sign in
- Which groups the user belongs to
- Which resources the user can access
- Which administrative roles the user has
- What security requirements must be satisfied before access is granted

Instead of managing every user's access separately inside every Microsoft application, Entra can be used as a centralized identity and access layer.

## Planned Entra Concepts

As the Enterprise Operations Hub develops, the project may demonstrate:

- User identities
- Security groups
- Group-based access
- Dynamic group membership where appropriate
- Role-based access control
- Least privilege
- Identity lifecycle management
- Conditional Access
- Access reviews
- Privileged Identity Management
- Identity governance
- Authentication controls
- Authorization controls
- Audit information

These capabilities will be introduced incrementally.

The initial V1 will not attempt to implement every Entra security or governance feature.

---

# 8. Group-Based Access Strategy

The project will favor group-based permissions where appropriate rather than assigning permissions individually to large numbers of users.

For example:

```text
Employee
    ↓
Microsoft Entra Security Group
    ↓
SharePoint Permission
    ↓
Enterprise Operations Hub
```

## Plain-English Explanation

Instead of giving SharePoint access directly to 500 individual employees, an administrator can give access to a security group.

Employees who belong to the appropriate group receive the corresponding access.

This makes permissions easier to manage, audit, automate, and eventually integrate with identity-governance processes.

If a user's Microsoft organizational account is disabled, that user can no longer authenticate normally to Microsoft 365 resources.

Group membership and account status are related identity-management concepts but represent different controls.

---

# 9. Power Apps Developer Plan

The Microsoft Power Apps Developer Plan has been activated using the organizational Microsoft 365 account.

A Power Platform developer environment was successfully created.

## Developer Environment

```text
Sean Reed's Environment
```

Microsoft identifies this environment as a:

**Developer Environment**

Microsoft also indicates that the environment is:

**Not intended for production use.**

## Plain-English Explanation

The developer environment gives us a safe place to build and experiment with Power Platform applications without treating the environment as a real production business system.

This is where we can learn, develop, test, break things, fix things, and document the process.

---

# 10. Power Apps

Power Apps will be used to create the user-facing request experience for the Enterprise Operations Hub.

## Initial Use Case

The first planned Power Apps use case is:

**SharePoint Access / Permission Change Request**

A user will eventually be able to submit information such as:

- Requested SharePoint resource
- Requested permission level
- Business justification
- Request type
- Additional comments
- Other information required by the approval process

The exact data fields will be determined during the V1 requirements and data-modeling phase.

## Plain-English Explanation

Power Apps will provide the form/application employees interact with.

Instead of asking employees to email IT saying:

> "Can you give me access to this SharePoint site?"

the application will provide a structured process for submitting the request.

That makes the request easier to approve, track, automate, report on, and audit.

---

# 11. Power Automate

Power Automate is available through the Microsoft Power Platform environment.

Power Automate will provide workflow automation for the Enterprise Operations Hub.

## Initial Workflow

The first planned workflow will support the:

**SharePoint Access / Permission Change Request**

The workflow is expected to eventually include:

1. Request submission
2. Request validation
3. Manager and/or resource-owner approval
4. Approval or rejection
5. Request status updates
6. User notifications
7. Administrative notifications
8. Audit history
9. Reminders
10. Escalation
11. Future automated provisioning where appropriate

## Plain-English Explanation

Power Apps collects the request.

Power Automate handles what happens **after the request is submitted**.

For example:

```text
Employee submits request
        ↓
Request is recorded
        ↓
Approver receives request
        ↓
Approver approves or rejects
        ↓
Request status changes
        ↓
Employee receives notification
        ↓
Action is recorded for auditing
```

Later versions may automate additional portions of the fulfillment process.

---

# 12. Dataverse

Dataverse capabilities are available through the Power Apps developer environment.

Dataverse will not automatically be used for every piece of project data simply because it is available.

## Plain-English Explanation

Dataverse is Microsoft's structured cloud data platform for Power Platform applications.

It provides more advanced relational data, security, business logic, and application capabilities than a basic SharePoint list.

However, adding more technology does not automatically make an application better.

The first version of Enterprise Operations Hub will use the simplest architecture capable of satisfying the business requirements.

Dataverse will be introduced when the project reaches requirements where relational data, advanced application security, or other Dataverse capabilities provide a clear advantage.

---

# 13. Power BI

Power BI is planned for a later phase of the project.

It will eventually provide reporting and analytics for operational information such as:

- Number of requests
- Request types
- Approval rates
- Rejection rates
- Request status
- Processing time
- SLA performance
- Access trends
- Outstanding requests
- Governance metrics

Power BI has not yet been implemented.

---

# 14. PowerShell

PowerShell is planned as an administrative and automation layer.

Future PowerShell capabilities may include:

- SharePoint administration
- Permission reporting
- User and group reporting
- Governance auditing
- Bulk administrative operations
- Identity reporting
- Automated administrative tasks

PowerShell has not yet been implemented in the Enterprise Operations Hub.

---

# 15. PnP PowerShell

PnP PowerShell is planned for SharePoint-specific administration and automation.

Potential uses include:

- Site configuration
- Permission auditing
- List and library management
- SharePoint reporting
- Site provisioning
- Governance checks
- Administrative automation

PnP PowerShell has not yet been implemented.

---

# 16. Microsoft Graph

Microsoft Graph is planned for a later development phase.

## Plain-English Explanation

Microsoft Graph is an API that allows applications and scripts to communicate programmatically with Microsoft cloud services.

Instead of an administrator manually clicking through Microsoft 365 interfaces, software can request information or perform approved actions through Graph.

Potential Enterprise Operations Hub uses include:

- Reading user information
- Reading group information
- Managing approved identity operations
- Retrieving Microsoft 365 information
- Automating administrative processes
- Supporting access governance
- Building reporting processes

Microsoft Graph has not yet been implemented.

---

# 17. Security and Identity Governance

Security will not be treated as an afterthought in the Enterprise Operations Hub.

As the project develops, the solution will incorporate security and identity-governance principles.

Potential concepts include:

- Least privilege
- Role-based access
- Group-based permissions
- Approval-based access
- Separation of duties
- Identity lifecycle management
- Access reviews
- Privileged access
- Permission auditing
- Logging
- Evidence collection
- Access revocation
- Security reporting

## Example Future Access Lifecycle

```text
User requests access
        ↓
Business justification provided
        ↓
Manager / resource owner reviews request
        ↓
Request approved or rejected
        ↓
Access provisioned
        ↓
Action recorded
        ↓
Access periodically reviewed
        ↓
Access retained or revoked
```

This transforms a simple permission request into an identity-governance process.

---

# 18. GRC Direction

Governance, Risk, and Compliance concepts will be incorporated into later project phases.

The goal is not simply to memorize security frameworks.

The goal is to demonstrate how security requirements can be translated into technical controls and operational processes.

The project is expected to explore alignment with:

- NIST Cybersecurity Framework 2.0
- CIS Controls
- ISO/IEC 27001 concepts

These frameworks have not yet been implemented or mapped to project controls.

They are documented here as part of the planned project direction.

## Future Control-Mapping Concept

A future project control may follow a structure similar to:

```text
Security Requirement
        ↓
Framework / Control
        ↓
Organizational Policy
        ↓
Technical Implementation
        ↓
Approval / Authorization
        ↓
Audit Evidence
        ↓
Testing
        ↓
Remediation
```

This will help demonstrate the connection between technical Microsoft administration and security governance.

---

# 19. Development Environment Strategy

The Enterprise Operations Hub follows this principle:

> Build the simplest working enterprise solution first, then introduce additional technology when there is a clear technical or business reason.

The initial V1 architecture will focus primarily on:

```text
SharePoint Online
        ↓
Power Apps
        ↓
Power Automate
```

Once that workflow operates successfully from beginning to end, additional layers can be introduced.

---

# 20. Planned Technology Progression

The current planned development order is:

1. SharePoint Online architecture
2. Power Apps
3. Power Automate
4. Dataverse
5. Power BI
6. PowerShell
7. PnP PowerShell
8. Microsoft Graph
9. Identity and security governance
10. Governance / security control mapping
11. C# / ASP.NET Core
12. Microsoft Azure

The order may change if project requirements provide a technical reason to do so.

---

# 21. Local Development Environment

The local project repository is stored on an external Crucial X9 drive.

Project directory:

```text
/Volumes/Crucial X9/Enterprise-Operations-Hub
```

Git has been initialized in the project directory.

The repository currently contains:

```text
Enterprise-Operations-Hub/
├── docs/
│   ├── architecture/
│   ├── requirements/
│   ├── sharepoint/
│   ├── power-apps/
│   ├── power-automate/
│   ├── dataverse/
│   ├── power-bi/
│   ├── powershell/
│   ├── graph/
│   ├── governance/
│   ├── testing/
│   └── environment-setup.md
├── screenshots/
├── scripts/
│   ├── powershell/
│   └── graph/
├── DEBUGGING_JOURNAL.md
├── PROJECT_JOURNAL.md
├── README.md
└── .gitignore
```

---

# 22. Source Control

Git is being used for local source control.

The repository has been initialized with:

```bash
git init
```

A `.gitignore` file has also been created.

The project is stored on an external macOS drive, which may create Apple metadata files beginning with `._`.

These files should not be committed to the repository.

The `.gitignore` currently includes:

```text
.DS_Store
._*
```

## Plain-English Explanation

Git keeps a history of changes made to the project.

This allows us to see what changed, when it changed, and eventually maintain versions of documentation, scripts, configuration information, and source code.

The `.gitignore` tells Git:

> "These files exist on my computer, but they are not part of the actual project, so don't track them."

---

# 23. Documentation Strategy

The project will maintain documentation throughout development rather than attempting to recreate the documentation after the project is finished.

Documentation includes:

- README
- Environment setup
- Architecture
- Requirements
- SharePoint design
- Power Apps implementation
- Power Automate workflows
- Dataverse design
- Power BI reporting
- PowerShell scripts
- Microsoft Graph implementation
- Governance documentation
- Testing documentation
- Project journal
- Debugging journal
- Screenshots

---

# 24. Project Journal

`PROJECT_JOURNAL.md` will document development progress and major project decisions.

Examples include:

- Environment creation
- Architecture decisions
- Features completed
- Technologies introduced
- Design decisions
- Milestones reached
- Changes in project direction

---

# 25. Debugging Journal

`DEBUGGING_JOURNAL.md` will document significant technical problems encountered during development.

Each useful debugging entry should eventually record:

- Problem
- Symptoms
- Cause
- Investigation
- Solution
- Verification
- Lesson learned

## Plain-English Explanation

The debugging journal is useful because solving problems is part of the portfolio.

A hiring manager should not only see that the final application works.

The documentation can also demonstrate:

> "I encountered this problem, investigated it, determined the cause, fixed it, and verified the solution."

---

# 26. V1 Business Use Case

The first end-to-end business process will be:

**SharePoint Access / Permission Change Request**

The initial goal is to demonstrate a complete workflow rather than building many incomplete features.

The user should eventually be able to:

1. Open the Enterprise Operations Hub.
2. Submit a SharePoint access or permission-change request.
3. Provide the required business information.
4. Submit the request.
5. Route the request to the appropriate approver.
6. Approve or reject the request.
7. Update the request status.
8. Notify the appropriate users.
9. Maintain a record of the request.
10. Provide information that can later support auditing and reporting.

---

# 27. V1 Success Criteria

The first major project milestone is:

> **SharePoint Online + Power Apps + Power Automate working end-to-end.**

Advanced technologies will not be allowed to distract from completing this milestone.

Once V1 works reliably, the project can progressively add:

- Dataverse
- Reporting
- PowerShell automation
- Microsoft Graph
- Entra identity governance
- Security controls
- GRC framework mapping
- Additional development technologies

---

# 28. Current Environment Status

| Component                            | Status       |
| ------------------------------------ | ------------ |
| Microsoft organizational account     | Active       |
| Microsoft 365 tenant                 | Active       |
| Microsoft 365 Business Basic         | Active       |
| SharePoint Online                    | Verified     |
| SharePoint Admin Center              | Verified     |
| Microsoft Entra ID                   | Available    |
| Power Apps Developer Plan            | Active       |
| Power Platform developer environment | Active       |
| Power Apps                           | Available    |
| Power Automate                       | Available    |
| Dataverse developer capabilities     | Available    |
| Power BI implementation              | Not started  |
| PowerShell implementation            | Not started  |
| PnP PowerShell implementation        | Not started  |
| Microsoft Graph implementation       | Not started  |
| NIST control mapping                 | Not started  |
| CIS Controls mapping                 | Not started  |
| C# / ASP.NET Core                    | Future phase |
| Microsoft Azure deployment           | Future phase |
| Local Git repository                 | Initialized  |
| Project documentation structure      | Created      |

---

# 29. Current Project Phase

The environment foundation has been established.

The next major phase is:

**SharePoint Online Architecture and V1 Requirements**

The next development work will define the SharePoint structure required to support the first SharePoint Access / Permission Change Request workflow.

---

# 30. Development Principle

The Enterprise Operations Hub will be built one layer at a time.

The project will prioritize:

- Working functionality over unnecessary complexity
- Understanding over copying
- Security by design
- Realistic enterprise architecture
- Documentation
- Testing
- Troubleshooting
- Automation
- Governance
- Maintainability

Technologies will only be presented as completed portfolio skills after they have actually been implemented, understood, and tested within the project.

```

```
