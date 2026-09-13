# Enterprise Operations Hub — Project Journal

This journal documents the development of the Enterprise Operations Hub from initial planning through implementation.

Entries record major milestones, technical decisions, configuration work, and lessons learned throughout the project.

---

## September 2026 — Project Foundation and Environment Setup

### Project Started

Development began on the **Enterprise Operations Hub**, an enterprise-style Microsoft 365 operations and request-management platform.

The project was created as a career portfolio project designed to combine existing Microsoft 365 and SharePoint administration experience with additional development, automation, identity, security, governance, and reporting technologies.

The first major milestone was defined as:

> **Build a working SharePoint Online + Power Apps + Power Automate request-management workflow from beginning to end.**

The first business process selected for implementation is:

**SharePoint Access / Permission Change Request**

This use case was selected because it represents a realistic enterprise IT process and provides a foundation for later identity governance and automation capabilities.

---

### Architecture Direction Established

The initial V1 architecture was defined as:

`````text
Employee
    ↓
SharePoint Online Portal
    ↓
Power Apps
    ↓
SharePoint Data
    ↓
Power Automate
    ↓
Approval Process
    ↓
IT / M365 Administration

Good. We're going to make the **first journal entry** cover the foundation work we've already completed. This is different from `environment-setup.md`: we're recording the **story of what we did**, including a couple of problems we encountered.

Copy and paste this entire block into `PROJECT_JOURNAL.md`:

````markdown
# Enterprise Operations Hub — Project Journal

This journal documents the development of the Enterprise Operations Hub from initial planning through implementation.

Entries record major milestones, technical decisions, configuration work, and lessons learned throughout the project.

---

## September 2026 — Project Foundation and Environment Setup

### Project Started

Development began on the **Enterprise Operations Hub**, an enterprise-style Microsoft 365 operations and request-management platform.

The project was created as a career portfolio project designed to combine existing Microsoft 365 and SharePoint administration experience with additional development, automation, identity, security, governance, and reporting technologies.

The first major milestone was defined as:

> **Build a working SharePoint Online + Power Apps + Power Automate request-management workflow from beginning to end.**

The first business process selected for implementation is:

**SharePoint Access / Permission Change Request**

This use case was selected because it represents a realistic enterprise IT process and provides a foundation for later identity governance and automation capabilities.

---

### Architecture Direction Established

The initial V1 architecture was defined as:

```text
Employee
    ↓
SharePoint Online Portal
    ↓
Power Apps
    ↓
SharePoint Data
    ↓
Power Automate
    ↓
Approval Process
    ↓
IT / M365 Administration
`````

Future versions may expand the architecture with:

```text
Dataverse
Microsoft Entra ID
Power BI
PowerShell
PnP PowerShell
Microsoft Graph
Identity Governance
Security / GRC Controls
C# / ASP.NET Core
Microsoft Azure
```

A key development decision was made not to introduce these technologies simply for the purpose of listing them on a resume.

Each technology should solve an actual project requirement and be implemented and tested before being presented as project experience.

---

### Microsoft 365 Tenant Established

A Microsoft 365 organizational environment was established for:

**Urban Assessory LLC**

Tenant domain:

```text
urbanassessory.onmicrosoft.com
```

An organizational Microsoft account was created for administration and development.

Microsoft 365 Business Basic was activated to provide the core Microsoft 365 services required for the project.

---

### SharePoint Online Verified

The SharePoint Admin Center was accessed successfully.

Active SharePoint sites were visible, confirming that SharePoint Online had been provisioned successfully for the tenant.

SharePoint Online will serve as the initial portal and data platform for V1.

---

### Microsoft Entra ID Available

Microsoft Entra ID is available as the tenant's cloud identity and access-management system.

Future project phases are expected to explore concepts such as:

- Security groups
- Group-based permissions
- Dynamic group membership where appropriate
- Role-based access control
- Least privilege
- Identity lifecycle management
- Access reviews
- Conditional Access
- Privileged Identity Management
- Identity governance

These capabilities are intentionally being deferred until the core V1 workflow is functional.

---

### Power Apps Developer Environment Established

The Microsoft Power Apps Developer Plan was activated using the organizational Microsoft account.

A dedicated developer environment was successfully created:

```text
Sean Reed's Environment
```

The environment is identified by Microsoft as a development environment and is not intended for production use.

This environment provides a location for developing and testing Power Platform components.

---

### Power Platform Capabilities Verified

The Power Apps maker portal was successfully accessed.

Available development areas included:

- Apps
- Tables
- Flows
- Solutions
- Power Platform development tools

Dataverse development capabilities are available through the developer environment.

A decision was made not to move the V1 data model into Dataverse automatically.

The initial architecture will use the simplest data platform that satisfies the requirements, with Dataverse introduced later when its capabilities provide a clear technical advantage.

---

### Local Project Repository Created

The local project repository was created on an external **Crucial X9** drive.

Project path:

```text
/Volumes/Crucial X9/Enterprise-Operations-Hub
```

Git was initialized using:

```bash
git init
```

The repository uses the `main` branch.

---

### Project Directory Structure Created

The following initial structure was established:

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

The structure separates documentation, screenshots, scripts, testing information, architecture decisions, and technology-specific implementation notes.

---

### Visual Studio Code Configured

Visual Studio Code is being used as the primary local editor.

An initial issue occurred when attempting to launch VS Code from Terminal using:

```bash
code .
```

The shell returned:

```text
zsh: command not found: code
```

The VS Code shell command was then installed into the macOS PATH using the VS Code Command Palette.

After installation, the project could be opened from Terminal using:

```bash
code .
```

This issue will also be recorded in the project's debugging journal.

---

### macOS Metadata Files Excluded From Git

Because the repository is stored on an external drive connected to macOS, Apple metadata files appeared in the project directory.

A `.gitignore` file was created containing:

```text
.DS_Store
._*
```

This prevents macOS metadata files from being tracked as part of the source repository.

Git status was checked afterward to verify that the unwanted metadata files were being ignored.

---

### Initial Documentation Created

The following core documentation files were established:

```text
README.md
PROJECT_JOURNAL.md
DEBUGGING_JOURNAL.md
docs/environment-setup.md
```

The README defines the overall project, business problem, technology direction, V1 objective, and planned architecture.

The environment setup document records the Microsoft 365, SharePoint, Power Platform, identity, and local development environment.

The Project Journal records development progress and technical decisions.

The Debugging Journal will document significant technical problems, their causes, solutions, and lessons learned.

---

### Security Documentation Rule Established

Sensitive information must not be committed to the project repository.

Examples include:

- Passwords
- Payment information
- Authentication tokens
- API keys
- Client secrets
- Private certificates
- Connection secrets

Future authentication and integration documentation should use placeholders rather than real credentials.

---

### Development Strategy

The project will be developed incrementally.

The guiding principle is:

> **Build the simplest working enterprise solution first, understand how it works, and then add additional technology when there is a clear reason for it.**

The project will prioritize:

- Understanding over copying
- Working functionality over unnecessary complexity
- Security by design
- Realistic enterprise processes
- Documentation
- Testing
- Troubleshooting
- Automation
- Governance
- Maintainability

---

### Current Status

**Foundation phase: Complete**

Completed:

- Microsoft 365 organizational tenant established
- Microsoft 365 Business Basic activated
- SharePoint Online verified
- Microsoft Entra ID available
- Power Apps Developer Plan activated
- Power Platform developer environment created
- Dataverse development capabilities available
- Local project repository created
- Git initialized
- VS Code configured
- Repository structure created
- README created
- Environment documentation created
- Project journal created
- Debugging journal prepared

### Next Phase

The next phase is:

**V1 SharePoint Architecture and Requirements**

The first implementation target will be the:

**SharePoint Access / Permission Change Request**

```

Then hit **⌘ + S**.

One small thing worth noticing: we're documenting the `code .` problem here because it was part of the project's history, but later we'll put the **technical troubleshooting details** in `DEBUGGING_JOURNAL.md`. That's the difference between the two journals.

```

## September 2026 — Access Requests SharePoint List Implemented

### Milestone

Implemented the initial V1 data structure for the SharePoint Access / Permission Change Request workflow in the Enterprise Operations Hub.

### SharePoint Implementation

Created the `Access Requests` list in the Enterprise Operations Hub SharePoint Online site and implemented the planned request, approval, fulfillment, and audit-related fields.

The list now captures:

- Request identification and requester information
- Target user
- Request type
- SharePoint resource and resource URL
- Requested permission level
- Business justification and additional comments
- Request lifecycle status
- Approver and approval decision
- Approval comments and approval timestamp
- Assigned administrator
- Fulfillment notes and fulfillment timestamp
- Completion timestamp
- Cancellation reason

### Governance Decisions

The standard permission request process limits requested permission levels to:

- Read
- Contribute
- Edit

Owner / Full Control access is intentionally excluded from the standard user access-request workflow and will require a separate elevated-access process.

Requester, Target User, Approver, and Assigned Administrator use SharePoint Person or Group columns so records are associated with Microsoft 365 identities rather than plain-text names.

Request Type, Requested Permission, Status, and Approval Decision use controlled Choice fields to improve data consistency and support future automation and reporting.

### Workflow Design

Approval and fulfillment are stored separately.

Approval represents authorization for the requested access change.

Fulfillment represents the technical action performed by the assigned Microsoft 365 / SharePoint administrator.

Separate timestamps are maintained for approval, fulfillment, and final completion to support future auditing and operational reporting.

### Current Status

The initial SharePoint V1 list schema is implemented.

Next steps will focus on validating the list behavior and preparing the SharePoint data layer for integration with Power Apps and Power Automate.

### Security and Governance Review

Reviewed the Access Requests list's Versioning and Advanced Settings before beginning automation.

Version history is enabled and configured to retain up to 50 versions of each list item. This provides additional auditability by preserving changes made to access-request records over time.

The current SharePoint item-level permission configuration allows users with sufficient list permissions to read and edit all items. This is acceptable during initial development and testing but is not the intended production security model.

The planned security model must account for multiple roles:

- Requesters should primarily access their own requests.
- Approvers must be able to access requests assigned to them.
- IT / Microsoft 365 administrators must be able to access requests they are responsible for fulfilling.
- Portal administrators require broader administrative access.

Item-level permissions will not be changed until the role and workflow permission model is implemented and tested, to avoid interfering with approval and fulfillment automation.

Quick property editing is currently enabled and will also be reviewed when the controlled Power Apps interface and security model are implemented.

SharePoint Content Approval remains disabled because approval will be handled through the custom Power Automate workflow rather than through a second SharePoint-native approval mechanism.

## September 12, 2026 — First Power Automate Workflow Successfully Tested

Completed and successfully tested the first working Power Automate workflow for the Enterprise Operations Hub.

### Flow

**Access Request - Initialize Request ID**

### Function

When a new item is created in the SharePoint **Access Requests** list, Power Automate:

1. Detects the newly created request.
2. Retrieves the SharePoint item ID.
3. Generates a formatted enterprise Request ID.
4. Updates the original SharePoint list item while preserving its existing data.

### Successful Test

Created:

**Test - HR Site Access**

SharePoint assigned the underlying item ID and Power Automate successfully generated:

`AR-00003`

Both Power Automate actions completed successfully:

- When an item is created — Succeeded
- Update item — Succeeded

### Milestone

This is the first successfully tested automation connecting the Enterprise Operations Hub SharePoint data layer with Power Automate.

The project now has a working automated process rather than only a manually configured SharePoint list.
