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
```

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

### Concept Learned — Software Architecture Layers vs. OSI Layers

While beginning the Power Apps portion of the project, I clarified the difference between software architecture layers and the OSI networking model.

In the Enterprise Operations Hub V1:

- **Power Apps** acts as the front-end / presentation layer. It provides the interface employees use to submit and interact with requests.
- **SharePoint Online** currently acts as the back-end data layer. The Access Requests list stores the request records.
- **Power Automate** provides workflow and business logic, such as generating Request IDs, changing request status, routing approvals, and sending notifications.

A simplified view is:

`Power Apps → SharePoint → Power Automate`

This use of the term "layer" should not be confused with the OSI networking model.

For example, SharePoint being the application's data layer does **not** mean it is OSI Layer 2. OSI Layer 2 is the Data Link layer and deals with technologies and concepts such as Ethernet frames, MAC addresses, switches, and VLANs.

Similarly, describing Power Apps as the application's presentation/front-end layer does not assign it an OSI layer number.

### Key Takeaway

The same terminology can have different meanings depending on context.

**Software architecture:** Front end → Back end/Data → Business Logic

**OSI networking:** Application → Presentation → Session → Transport → Network → Data Link → Physical

Understanding which architectural model is being discussed prevents confusing application development concepts with networking concepts.

## September 13, 2026 — Power Apps V1 Development Started

Created the initial Power Apps application for the Enterprise Operations Hub and connected it to the SharePoint `Access Requests` list.

### Completed

- Created the Power App `Enterprise Operations Hub - Access Requests`.
- Connected the app to the SharePoint `Access Requests` data source.
- Verified existing SharePoint request records load into the app.
- Reviewed the generated `RecordsGallery1` gallery.
- Confirmed `Form1` uses `RecordsGallery1.Selected` as its Item property.
- Reviewed the form's New, Edit, and View modes.
- Reviewed the generated Power Fx logic used by the New Request control.
- Verified that selecting `+ New` successfully opens `Form1` in New mode.
- Identified that the generated form currently exposes both employee-facing and administrative/workflow fields.

### Key Concepts Learned

- SharePoint acts as the application's data layer while Power Apps provides the user-facing application interface.
- Galleries display collections of records.
- `RecordsGallery1.Selected` represents the currently selected SharePoint record.
- Forms can dynamically switch between `FormMode.New`, `FormMode.Edit`, and `FormMode.View`.
- Power Fx variables such as `newMode` and `editMode` can control application state.
- `NewForm(Form1)` prepares the form to create a new SharePoint record.
- `UpdateContext({ newMode: true })` changes local application state.

### Current Checkpoint

The generated New Access Request form is functional but has not yet been customized.

Next session: determine which fields should be employee-editable versus system/workflow-controlled, then customize the New Request experience accordingly.

## September 13, 2026 — First End-to-End Access Request Submission

### Milestone

Completed the first successful end-to-end submission through the Enterprise Operations Hub Power Apps interface.

### Work Completed

- Configured the employee-facing Access Request form.
- Automatically populated the Requester with the currently signed-in user.
- Corrected SharePoint Person fields to display the user's friendly display name instead of the raw Claims value.
- Verified Request Type and Requested Permission choice fields.
- Confirmed required and optional field behavior.
- Configured new requests to receive a default Status of `Draft`.
- Successfully submitted a new request from Power Apps to the SharePoint `Access Requests` list.
- Verified that the existing Power Automate flow automatically generated the Request ID.

### Successful Test

Test request:

`Test - Operations Site Access`

Generated Request ID:

`AR-00004`

### Verified V1 Data Flow

Power Apps → SharePoint Online → Power Automate → Request ID generation

### Result

The project now has a functioning request intake process. An employee can create an access request through the Power Apps interface, the request is stored in SharePoint, and Power Automate assigns the request a standardized tracking ID.

### Next Phase

Build the approval workflow so submitted access requests can move from request intake into manager/authorized approver review.

---

## September 14, 2026 — Approval Workflow Completed and Tested

### Objective

Build and validate the approval stage of the SharePoint Access Request process so that submitted requests can be reviewed by an authorized approver and automatically updated based on the approver's decision.

### Power Automate Approval Workflow

Created and configured the Power Automate flow:

`Access Request - Approval Workflow`

The workflow now follows this process:

Power Apps → SharePoint Access Requests List → Power Automate → Approval Request → Approver Decision → Condition → SharePoint Update

### Approval Process

The flow performs the following actions:

1. Detects when a new Access Request item is created in SharePoint.
2. Initializes the workflow fields for the request.
3. Sends an approval request using **Start and wait for an approval**.
4. Waits for the authorized approver to select **Approve** or **Reject**.
5. Evaluates the approval **Outcome** using a Power Automate Condition.
6. Routes the request through the appropriate True or False branch.
7. Updates the original SharePoint list item with the approval results.

### Approved Branch

Condition:

`Outcome = Approve`

When the condition is True, Power Automate updates the request with:

- Status: Approved
- Approval Decision: Approved
- Approver: Approval responder
- Approval Comments: Comments entered by the approver
- Approval Date: Approval response date

The approved branch was successfully tested end-to-end.

Test request:

`Approval Test - Approved Path`

The SharePoint Access Requests list correctly recorded the approval decision, approver, comments, and approval date.

### Rejected Branch

When the approval Outcome is not Approve, the Condition follows the False branch.

Power Automate updates the request with:

- Status: Rejected
- Approval Decision: Rejected
- Approver: Approval responder
- Approval Comments: Comments entered by the approver
- Approval Date: Approval response date

The rejected branch was successfully tested end-to-end.

Test request:

`Approval Test - Rejected Path`

Approval comment used during testing:

`Rejected for workflow testing.`

The SharePoint Access Requests list correctly recorded the rejected status, approver, decision, comments, and approval date.

### Verified Approval Data Flow

Power Apps
→ SharePoint Online
→ Power Automate
→ Microsoft Approvals
→ Human Approver
→ Power Automate Condition
→ Approved / Rejected Branch
→ SharePoint Online

### Key Architecture Concept

Approval and fulfillment are intentionally separated.

**Approval** determines whether the requested access is authorized.

**Fulfillment** is the administrative action that actually grants, changes, or removes the requested SharePoint permissions.

This separation reflects an enterprise access-management process and provides a clearer audit trail between authorization and administrative execution.

### Result

The Enterprise Operations Hub now has a functioning request intake and approval process.

An employee can submit a SharePoint access request through Power Apps, the request is stored in SharePoint, a Request ID is generated, an approval is sent to an authorized approver, and the final approval decision is automatically written back to the SharePoint request record.

Both the **Approved** and **Rejected** workflow paths have been successfully tested.

### Next Phase

Build the fulfillment stage for approved requests so that an administrator can process the authorized SharePoint access change and record the fulfillment details.

---

## September 16, 2026 — My Requests View and Published App Validation

### Objective

Continue improving the employee-facing Power Apps experience by separating the user's personal requests from the broader request-management view and validating the behavior in the published application.

### My Requests Mode

Added application mode logic using the `varAppMode` variable.

The application can now distinguish between:

- `myrequests` — employee-facing view
- `allrequests` — broader administrative/request-management view

The application startup configuration was tested by temporarily switching between the two modes.

The final default mode was restored to:

```powerfx
Set(varAppMode, "myrequests")
```

### Request Filtering

Updated the Access Requests gallery so that when the application is running in `myrequests` mode, the gallery filters records based on the currently signed-in user's email address.

This allows an employee to see requests associated with their own account instead of automatically exposing every request in the SharePoint list.

The gallery continues to support text searching by request title.

### Delegation Warning

Power Apps initially displayed delegation warnings related to the `Search()` portions of the gallery formula.

The formula was adjusted and the warnings were cleared during development.

This troubleshooting reinforced the importance of considering delegation when designing Power Apps that may eventually operate against larger enterprise data sets.

### Person Field Display Fix

During live-app testing, the SharePoint Person fields for **Requester** and **Target User** initially displayed the underlying SharePoint claims identity format:

`i:0#.f|membership|user@domain`

instead of the user's friendly display name.

The Person-field display configuration was corrected so that the application displays the user's `DisplayName`.

Verified in the published application:

- Requester displays as `Sean Reed`
- Target User displays as `Sean Reed`
- Gallery requester information displays as `Sean Reed`
- Raw SharePoint claims strings are no longer displayed to the end user

### Published Application Validation

Saved and published the updated Power Apps canvas application.

The live application initially continued displaying the previous version while the newly published version propagated.

After the new version became available and the application reloaded, the updated Person-field display behavior was verified successfully in the live application.

### Result

The employee-facing application now has the foundation for a dedicated **My Requests** experience.

The application can distinguish between employee and broader request-management modes, filter the request gallery for the signed-in user, and display SharePoint Person fields using readable names instead of internal claims identifiers.

### Next Phase

Continue refining the My Requests experience and then build the fulfillment stage of the request lifecycle:

`Approved → In Progress → Completed`

The fulfillment stage will remain separate from approval so that authorization and administrative execution maintain distinct audit records.

## September 17, 2026 — Administrator Fulfillment Lifecycle Completed

### Objective

Extend the SharePoint access request process beyond approval by implementing and validating the administrator fulfillment and request-closure stages.

The goal was to preserve a clear separation between authorization and fulfillment so that an approved request does not automatically imply that the requested access change has been performed.

### Fulfillment Lifecycle

Validated the following request lifecycle:

`Approved → In Progress → Fulfilled → Completed`

Used the existing approved test request:

- Request ID: `AR-00008`
- Request Title: `Approval Test - Approved Path`
- Requested Permission: `Read`
- SharePoint Resource: `Executive Team Site`

### Administrator Assignment

After approval, the request was assigned to an administrator for fulfillment.

Updated:

- Status: `In Progress`
- Assigned Administrator: `Sean Reed`

The existing approval information remained unchanged, preserving the authorization audit trail.

### Manual Fulfillment

For V1, the actual SharePoint permission change is represented as a manual administrative action rather than an automated permission modification.

Recorded the following fulfillment information:

- Fulfillment Notes: `Granted Read access to the Executive Team Site for the approved target user. Access was fulfilled manually in accordance with the approved request.`
- Fulfillment Date: `September 17, 2026`

This maintains separation between the approval decision and the administrator responsible for executing the approved request.

### Request Closure

After fulfillment was recorded, the request was formally closed.

Updated:

- Status: `Completed`
- Completed Date: `September 17, 2026`

Cancellation Reason remained blank because the request was successfully fulfilled.

### Audit Trail Validation

Verified that the completed request preserved information from each stage of the process:

- Approval Decision: `Approved`
- Approver: `Sean Reed`
- Approval Comments retained
- Approval Date retained
- Assigned Administrator: `Sean Reed`
- Fulfillment Notes retained
- Fulfillment Date retained
- Completed Date recorded
- Final Status: `Completed`

This demonstrates separation between:

`Request Submission → Authorization → Administrative Fulfillment → Closure`

### Result

The Enterprise Operations Hub now supports the complete V1 SharePoint access-request lifecycle from submission through final closure.

The project can demonstrate that an approved request is not considered fulfilled until an administrator performs and records the requested action, and that fulfillment is distinct from formally closing the request.

### Next Phase

Improve the administrator-facing fulfillment experience so administrators can process approved requests through a controlled interface instead of directly editing workflow fields in the raw SharePoint list.

Future phases can then extend fulfillment with Power Automate, PnP PowerShell, and Microsoft Graph while preserving the same approval and audit model.

## September 18, 2026 — Fulfillment UI Hardening and V1 Finalization

Continued final V1 hardening of the Enterprise Operations Hub Power Apps fulfillment experience.

### Completed

- Validated the controlled fulfillment lifecycle: Approved → In Progress → Completed.
- Verified administrator assignment, fulfillment notes, fulfillment date, and completed date persist correctly.
- Restricted administrative fulfillment fields to Admin mode.
- Verified requester mode keeps workflow Status read-only and hides administrator-only fulfillment fields.
- Corrected the Assigned Administrator Person field to display the user's friendly DisplayName instead of SharePoint claims data.
- Simplified Completed Date and Fulfillment Date to date-only values and removed unnecessary 00:00 time controls.
- Improved the Power Apps layout by adding bottom spacing to the main form container for a cleaner finished interface.

### V1 Status

V1 is now in final validation and presentation cleanup. Remaining work includes final persistence testing, requester/admin mode finalization, publishing, documentation cleanup, screenshots, and final V1 repository updates.

## September 21, 2026 — Role-Aware Navigation and Final V1 Validation

### Objective

Complete final V1 validation of the requester and administrator experiences in the Enterprise Operations Hub Power App.

### Work Completed

- Added role-aware application startup behavior using Microsoft 365 group membership.
- Configured the application to default to the `myrequests` experience when it starts.
- Added an administrator authorization check using the Office 365 Groups connector.
- Verified the signed-in user's email against members of the designated administrator group.
- Configured the Admin View button so it is displayed only when the current user passes the administrator group check.
- Validated navigation between My Requests and Admin View.
- Confirmed My Requests displays requests belonging to the signed-in requester.
- Confirmed Admin View displays requests in the Approved, In Progress, and Completed fulfillment stages.
- Verified administrative fulfillment fields remain hidden from the normal requester experience.
- Verified Status remains visible to requesters but is read-only.
- Re-tested date-only fields and confirmed saved fulfillment and completion dates persist correctly.
- Confirmed Assigned Administrator displays the administrator's friendly display name instead of the SharePoint claims value.
- Performed fresh application startup testing after running `App.OnStart`.

### Role-Aware Startup Logic

The application initializes in requester mode and determines administrator access using Microsoft 365 group membership.

```powerfx
Set(varAppMode, "myrequests");

Set(
    varIsAdmin,
    !IsBlank(
        LookUp(
            Office365Groups.ListGroupMembers(
                "4ca05468-5622-4647-9108-271e7aafa7a0"
            ).value,
            Lower(mail) = Lower(User().Email)
        )
    )
)
```

The Admin View button uses:

```powerfx
varIsAdmin
```

This prevents the administrative navigation option from being presented to users who do not pass the administrator group-membership check.

### Validation Result

Fresh application startup testing completed successfully.

The application:

1. Opens in My Requests mode.
2. Displays the signed-in requester's requests.
3. Determines administrator eligibility through Microsoft 365 group membership.
4. Displays Admin View for an authorized administrator.
5. Allows the administrator to switch into the controlled fulfillment experience.
6. Keeps administrative fulfillment controls out of the normal requester experience.

### Security Note

The current role-aware controls provide application-level user experience protection. They should not be treated as a replacement for SharePoint data-layer authorization.

A user with sufficient direct permissions to the underlying SharePoint list could potentially interact with data outside of the Power Apps interface.

Stronger data-layer enforcement can be introduced in later versions through SharePoint permission architecture, Dataverse security roles, Microsoft Entra ID, Microsoft Graph, and other governance controls.

### V1 Status

Enterprise Operations Hub V1 is now in final release preparation.

Core V1 functionality has been validated:

- Request submission
- Automatic Request ID generation
- Approval and rejection workflow
- Requester-specific My Requests experience
- Role-aware administrator navigation
- Approved → In Progress → Completed fulfillment lifecycle
- Administrator assignment
- Fulfillment documentation
- Date persistence
- Friendly Person-field display
- Requester/admin interface separation

### Next Step

Save and publish the validated Power Apps version, perform the final end-to-end V1 test, and prepare the project for its V1 portfolio release.

## September 21, 2026 — V1 Published and Live Application Validated

### Objective

Complete final V1 validation of the Enterprise Operations Hub Access Requests application and publish the tested version for portfolio demonstration.

### Final V1 Hardening

Before publication, the administrative fulfillment fields were hardened so they require both an authorized administrator and the Admin View application mode.

The following administrative fields now use:

```powerfx
varIsAdmin && varAppMode = "admin"
```

Applied to:

- Assigned Administrator
- Completed Date
- Fulfillment Date
- Fulfillment Notes

This prevents the administrative fulfillment fields from appearing in the requester experience even if the application mode is changed unexpectedly.

Status remains visible to requesters as a read-only workflow field.

### Role-Aware Startup Validation

`App.OnStart` was executed and validated successfully.

The application initializes in requester mode:

```powerfx
Set(varAppMode, "myrequests");
```

Administrator authorization is determined through Microsoft 365 group membership using the Office365Groups connector.

The authorized administrator account successfully passed the group-membership check and received access to the Admin View navigation option.

### Requester Experience Validation

The application was tested in My Requests mode before publication.

Validation confirmed:

- My Requests is the default application experience.
- The requester sees only requests associated with the signed-in account.
- Status remains visible.
- Administrative fulfillment fields remain hidden.
- Admin View is available only when the signed-in account passes the administrator group-membership check.

### Administrator Experience Validation

Admin View was tested successfully before publication.

Validation confirmed:

- Admin View displays the administrator fulfillment record set.
- Approved, In Progress, and Completed requests can be surfaced for administrative processing.
- Administrative fulfillment information is visible to the authorized administrator.
- Assigned Administrator displays a friendly user name instead of SharePoint claims data.
- Completed Date and Fulfillment Date display as date-only values.
- Fulfillment Notes remain available as part of the fulfillment audit trail.

### Publication

The tested V1 application was published successfully on September 21, 2026.

Application:

**Enterprise Operations Hub - Access Requests**

A Power Apps description was added describing the application as an enterprise request-management solution built with Power Apps, SharePoint Online, Power Automate, and Microsoft 365 group-based role awareness.

### Published Application Validation

The application was launched through the Power Apps Play experience after publication.

Power Apps initially loaded a cached older version and displayed a notification that a newer version was available. The application was refreshed using the Power Apps refresh control before final testing.

The current published version was then validated successfully.

Published requester-mode validation confirmed:

- My Requests loads as the default experience.
- Requester records load successfully.
- Administrative fulfillment fields remain hidden.
- The authorized administrator account receives the Admin View option.

Published administrator-mode validation confirmed:

- Admin View switches to the administrator record set.
- Completed fulfillment records load successfully.
- Status displays correctly.
- Assigned Administrator displays correctly.
- Completed Date persists and displays correctly.
- Fulfillment Date persists and displays correctly.
- Fulfillment Notes persist and display correctly.

A completed test request displayed the expected fulfillment information in the live published application.

### Security Note

The role-aware Power Apps controls implemented in V1 provide application-level user-interface protection and workflow separation.

They do not replace SharePoint data-layer permissions or enterprise authorization controls.

Future versions can strengthen enforcement through SharePoint permission architecture, Dataverse security roles, Microsoft Graph, PnP PowerShell, Entra ID, and additional governance controls.

### V1 Result

The core V1 workflow is now implemented, published, and validated through the live Power Apps experience:

**Request Submission → Request ID Generation → Approval / Rejection → Administrator Fulfillment → Completion**

V1 demonstrates:

- SharePoint Online request management
- Power Apps requester and administrator experiences
- Power Automate approval workflows
- Microsoft 365 group-aware navigation
- Controlled manual fulfillment lifecycle
- Person-field handling
- Workflow status management
- Date persistence
- Fulfillment documentation
- Role-aware user-interface controls
- Published application validation

The functional Power Apps portion of V1 is now ready to be frozen while final portfolio documentation, screenshots, README updates, and presentation materials are completed.

### Next Phase

Complete final V1 portfolio packaging:

- Capture portfolio-quality screenshots.
- Update README with final V1 implementation status.
- Review architecture and requirements documentation for accuracy.
- Commit final V1 documentation to GitHub.
- Prepare the Enterprise Operations Hub portfolio presentation.
- Freeze V1 before beginning V2 operational enhancements.

## 2026-09-28 — V2 Dashboard Metrics Architecture

- Began development of the Operations Dashboard in Power Apps.
- Identified SharePoint delegation warnings caused by using `CountRows()` against the Access Requests list.
- Decided to correct the underlying architecture rather than leave delegation warnings in the application.
- Created a SharePoint `Request Metrics` list to store dashboard totals for Total Requests, Pending Approval, Approved, In Progress, and Completed.
- Began building the `Access Request - Update Dashboard Metrics` Power Automate flow.
- Configured the flow to trigger when an item is created or modified in the `Access Requests` list.
- Next step: retrieve Access Requests with the SharePoint `Get items` action and calculate/update the dashboard metrics.

## 2026-09-29 — V2 Dashboard Metrics Automation

- Built the `Access Request - Update Dashboard Metrics` Power Automate flow.
- Configured the flow to run when an item is created or modified in the SharePoint `Access Requests` list.
- Added server-side OData queries for Pending Approval, Approved, In Progress, and Completed request statuses.
- Added retrieval of total Access Requests and the `Dashboard Metrics` record from the `Request Metrics` SharePoint list.
- Added an Update Item action to write calculated request counts into the dashboard metrics record.
- Configured Power Automate expressions to calculate Total Requests, Pending Approval, Approved, In Progress, and Completed counts.
- Next step: test the automation end-to-end and connect the Power Apps Operations Dashboard to the Request Metrics data.

## 2026-09-30 — V2 Operations Dashboard Metrics Completed

- Completed and tested the Operations Dashboard metrics architecture.
- Connected the Power Apps dashboard to the SharePoint `Request Metrics` list.
- Replaced direct `CountRows()` calculations against `Access Requests` with precomputed metrics retrieved using `LookUp()`.
- Eliminated Power Apps delegation warnings from Total Requests, Pending Approval, Approved, In Progress, and Completed dashboard metrics.
- Added `Refresh('Request Metrics')` to `OperationsDashboardScreen.OnVisible` so the dashboard retrieves current metrics whenever the screen is opened.
- Performed an end-to-end status transition test from Pending Approval → Approved and verified the dashboard metrics updated correctly.
- Enabled pagination on the Power Automate `Get Total Requests` action with a 5,000-item threshold to provide a defined scaling boundary for the current V2 implementation.
- Retested the automation after enabling pagination using an Approved → In Progress transition.
- Verified the final SharePoint metrics: Total Requests = 10, Pending Approval = 0, Approved = 0, In Progress = 1, Completed = 2.
- Confirmed the complete pipeline: Access Requests → Power Automate → Request Metrics → Power Apps Operations Dashboard.
- Documented the remaining Power Automate performance advisory: `Get Total Requests` intentionally retrieves the complete request set, so the current V2 design has a documented 5,000-item aggregation boundary.

---

## October 2, 2026 — V2 Recent Activity and Dashboard Automation

### Recent Activity Pipeline Validated

Continued development of the V2 Operations Dashboard and validated the Recent Activity architecture end-to-end.

Current activity pipeline:

**Access Requests → Power Automate → Request Activity → Power Apps Operations Dashboard**

Validated that meaningful request status changes automatically create activity-history records and appear in the Power Apps Recent Activity gallery.

Successfully tested:

- Approved
- Rejected
- In Progress
- Completed
- Pending Approval

A negative test also confirmed that editing an unrelated field without changing Status does not create an activity-history event.

### Dashboard Refresh Improved

Updated `OperationsDashboardScreen.OnVisible` to refresh both dashboard data sources:

````powerfx
Refresh('Request Activity');
Refresh('Request Metrics');


### 2. Save it

Press:

**Ctrl + O**

Then press **Enter** to confirm the filename.

Then:

**Ctrl + X**

to exit Pico.

### 3. Immediately check Git

Run:

```bash
git status

## V2 — SLA and Priority Requirements Design — 2026-10-03

### Design Decisions
- Priority belongs to the Access Request as part of its operational state. The Operations Dashboard displays and acts on this data but does not own it.
- Initial priority should be determined from request type/business rules rather than relying solely on requester-selected urgency.
- Priority will determine the applicable SLA target.
- Authorized administrators/technicians may override priority when business circumstances change.
- Priority overrides should preserve the previous priority, new priority, actor, timestamp, and reason in the audit/activity history.
- Override reasons should use standardized selections where possible, with an **Other** option for a custom explanation.
- Changing priority should recalculate the applicable SLA deadline.
- Approval and fulfillment are separate operational responsibilities. Future SLA design should distinguish time waiting for authorization from fulfillment performance.
- The previous operational workflow of repeated approval follow-ups and eventual closure when approval is not received will inform future approval-SLA design but is not yet an implemented V2 rule.
- Completing a request should stop the SLA clock while preserving the final SLA result (**Met** or **Breached**) for historical auditing and reporting.
- Preserved SLA results can later support reporting such as SLA compliance percentage, resolution time, breaches by priority/request type, and escalation trends.

### Planned Implementation
Request Type → Priority → SLA Due Date → SLA Status → Operations Dashboard indicators

**Status:** DESIGN / PLANNED — not yet implemented.

## 2026-10-04 — V2 SLA Initialization and Policy-Driven Automation

### Completed
- Created the `SLA Policies` SharePoint configuration list.
- Defined configurable SLA policies for Critical, High, Normal, and Low priorities.
- Separated SLA target duration from duration unit and At Risk threshold.
- Created the `Access Request - Initialize SLA` Power Automate flow.
- Configured the flow to retrieve the SLA policy matching the Access Request priority.
- Added validation to confirm a matching SLA policy was returned.
- Configured the flow to preserve unrelated Access Request business state rather than overwrite approval, fulfillment, status, or cancellation data.
- Configured SLA initialization to set `SLA Status` to `Within SLA`.
- Implemented automatic SLA Due Date calculation using the request Created timestamp and the Target Duration retrieved from `SLA Policies`.
- Successfully validated the Normal-priority SLA initialization with test request `AR-00019`.

### Architecture Decisions
- SLA business rules are stored in `SLA Policies` rather than hard-coded into Power Automate.
- Power Automate is responsible for orchestration; SharePoint configuration data defines the SLA policy.
- Changing an SLA target should be a configuration change rather than require redesigning the automation.
- The SLA initialization flow owns SLA initialization fields and preserves unrelated request state.
- SLA initialization and SLA monitoring are separate responsibilities.
- A request can become overdue solely because time passes, so overdue detection should not depend only on item-created or item-modified triggers.

### Next
- Build a scheduled SLA evaluation flow.
- Detect requests approaching their At Risk threshold.
- Detect overdue requests.
- Update SLA Status without modifying unrelated request state.
- Surface At Risk and Overdue requests on the Operations Dashboard.
Great. Now paste this **directly underneath the existing `### Next` section**. This records what we actually built and validated after that plan.

```markdown
## 2026-10-04 — V2 Scheduled SLA Evaluation and Overdue Dashboard Indicator

### Completed

Continued development of the V2 SLA capability by implementing time-driven SLA monitoring and surfacing overdue requests on the Operations Dashboard.

Created and validated the scheduled Power Automate flow:

`Access Request - Evaluate SLA`

The flow runs once per hour and evaluates active Access Requests to determine whether their SLA deadline has passed.

### Scheduled SLA Evaluation Architecture

The evaluation process follows:

Access Requests → Scheduled Power Automate Evaluation → SLA Status Update

The flow retrieves requests using the following filter:

```text
Status ne 'Completed' and Status ne 'Rejected' and Status ne 'Cancelled'
````

This prevents terminal requests from being unnecessarily evaluated during each scheduled run.

For each remaining request, the flow evaluates whether:

- `SLA Due Date` contains a value.
- `SLA Due Date` is earlier than the current time.
- The request remains in an active operational state.

When these conditions are satisfied, the flow updates:

```text
SLA Status = Overdue
```

The flow preserves unrelated request fields and business state.

### Architecture Decision — Time-Driven Evaluation

SLA monitoring was intentionally separated from SLA initialization.

The initialization flow determines the original SLA deadline when a request is created.

The scheduled evaluation flow determines whether that deadline has subsequently been exceeded.

This separation is necessary because a request can become overdue simply because time passes. No SharePoint item modification is required for an SLA breach to occur.

### Dashboard Metrics Extended

Extended the existing:

`Access Request - Update Dashboard Metrics`

flow with a new:

`Get Overdue Requests`

aggregation step.

The dashboard metrics pipeline now includes overdue-request information:

Access Requests → Power Automate → Request Metrics → Power Apps Operations Dashboard

The `Request Metrics` SharePoint list was extended to store the current Overdue count.

During implementation, the Overdue query initially failed because the SharePoint display name was mistaken for the column's internal name.

The correct internal field name was identified as:

```text
SLA_x0020_Status
```

The working OData query is:

```text
SLA_x0020_Status eq 'Overdue'
```

The detailed troubleshooting process is documented separately in `DEBUGGING_JOURNAL.md`.

### Power Apps Operations Dashboard Updated

Added an `Overdue` KPI to the Operations Dashboard.

The dashboard now displays:

- Total Requests
- Pending Approval
- Approved
- In Progress
- Completed
- Overdue

The Overdue value is retrieved from the precomputed `Request Metrics` data rather than calculated directly against the operational `Access Requests` list in Power Apps.

This preserves the existing V2 architecture in which aggregation responsibility remains outside the presentation layer.

### Validation

End-to-end testing confirmed:

- The scheduled SLA evaluation flow runs successfully.
- Active requests with expired SLA Due Dates can be marked `Overdue`.
- Terminal requests are excluded from scheduled SLA evaluation.
- The dashboard metrics flow successfully counts overdue requests.
- `Request Metrics` stored `Overdue = 1`.
- Power Apps successfully retrieved the updated metric.
- The Operations Dashboard displayed `1 Overdue`.
- Existing Total, Pending Approval, Approved, In Progress, and Completed metrics continued functioning.

### Architecture Learning

This implementation separates five distinct responsibilities:

1. `Access Requests` stores current operational request state.
2. SLA initialization assigns the applicable deadline.
3. Scheduled SLA evaluation detects time-based SLA breaches.
4. Power Automate aggregates operational metrics into `Request Metrics`.
5. Power Apps presents the resulting operational information.

This prevents the Power Apps interface from becoming responsible for business-rule execution, time-based monitoring, and large-scale aggregation.

### Current V2 Status

The following V2 dashboard capabilities are now implemented and validated:

- Precomputed operational KPI metrics
- Recent Activity history
- SLA initialization
- Scheduled overdue evaluation
- Overdue request aggregation
- Overdue KPI presentation

Remaining V2 development includes:

- At Risk SLA evaluation
- Additional filtering
- Notifications
- Reporting / Power BI integration
- Additional request-management metrics
- Documentation, testing, and final interface refinement

```

This entry is important because it shows that we're no longer just building individual Power Automate flows. We're documenting **why responsibilities are separated across the architecture**—which is exactly the kind of reasoning you want to be able to explain in an engineer/architect interview.

Once you've pasted and saved that, tell me **done**. Then we'll decide whether to document the Power Apps formula issue separately or move forward.
```

## 2026-10-05 — SLA Evaluator Validation

### Completed

- Completed the Power Automate `Access Request - Evaluate SLA` flow.
- Configured scheduled evaluation of Access Requests.
- Implemented SLA status evaluation using:
  - SLA Due Date
  - SLA At Risk Date
  - Current UTC time
- Preserved existing SharePoint item values during automated updates.
- Validated the SLA state transitions:
  - Within SLA
  - At Risk
  - Overdue

### Testing

Created `Test - SLA At Risk Immediate` with:

- Priority: Normal
- SLA Due Date: October 6, 2026
- SLA At Risk Date: October 5, 2026

Manually ran the SLA evaluator and confirmed:

- The request entered the At Risk conditional branch.
- The SharePoint Update Item action executed successfully.
- SLA Status changed from `Within SLA` to `At Risk`.

### Result

The Enterprise Operations Hub can now automatically evaluate active access
requests and update their SLA status as deadlines approach or pass.

### Next

- Add SLA notifications and escalation logic for At Risk and Overdue requests.

### SLA At Risk Notification Validation

Added an Outlook notification to the `Access Request - Evaluate SLA` flow for requests that enter the `At Risk` state.

The notification includes:

- Request ID
- Request Title
- Priority
- SLA Status
- SLA At Risk Date
- SLA Due Date

Validation performed using request `AR-00020` (`Test - SLA At Risk Normal`).

Confirmed the complete automation path:

1. Scheduled SLA evaluator retrieved the active request.
2. Overdue condition evaluated False.
3. At Risk condition evaluated True.
4. SharePoint `Update item` completed successfully.
5. Outlook `Send an email (V2)` completed successfully.
6. SLA alert email was delivered to the Microsoft 365 mailbox.

Result: SLA At Risk notification functionality is working end-to-end.

Future polish:

- Format SLA dates from UTC/ISO format into a user-friendly local date/time format.
- Consider role-based notification recipients instead of the current test mailbox.
## 2026-10-07 — SLA Overdue Escalation & Duplicate Notification Prevention

### Completed

Enhanced the `Access Request - Evaluate SLA` flow to support SLA escalation while preventing repeated notifications during scheduled evaluations.

Updated the Overdue condition to require:

- SLA Due Date is not null.
- SLA Due Date is earlier than the current UTC time.
- SLA Status is not already `Overdue`.

Updated the At Risk condition to require:

- SLA At Risk Date is not null.
- SLA At Risk Date is earlier than the current UTC time.
- SLA Status is not already `At Risk`.

### Overdue Escalation

Added an Office 365 Outlook `Send an email (V2)` action to the Overdue branch.

The escalation email includes:

- Request ID
- Request Title
- Priority
- SLA Status
- SLA At Risk Date
- SLA Due Date

Overdue notifications are marked as High Importance.

### Validation

Validated the evaluator against test requests `AR-00020` and `AR-00021`.

Confirmed the complete Overdue automation path:

1. Scheduled SLA evaluator retrieved active requests.
2. Due Date was compared with the current UTC time.
3. Existing SLA Status was checked to prevent duplicate escalation.
4. Eligible requests transitioned to `Overdue`.
5. SharePoint `Update item` completed successfully.
6. Outlook `Send an email (V2)` completed successfully.
7. SLA Overdue escalation emails were delivered to the Microsoft 365 mailbox.

Confirmed that subsequent evaluator runs do not resend the Overdue notification when the request already has an SLA Status of `Overdue`.

### Result

The SLA evaluator now supports controlled state transitions:

`Within SLA → At Risk → Overdue`

Notifications are tied to the transition into At Risk or Overdue rather than being repeatedly sent on every scheduled evaluator run.

### Future Enhancements

- Format SLA dates from UTC/ISO into a user-friendly local date/time format.
- Add an operational priority/escalation queue for unresolved Overdue requests.
- Track how long requests remain Overdue.
- Define escalation behavior for requests that remain unresolved for multiple days.
- Consider role-based notification recipients instead of the current test mailbox.

## 2026-10-07 — SLA Notification & Duplicate Suppression Validation

### Completed

- Completed and validated automated SLA notifications in the Power Automate `Access Request - Evaluate SLA` flow.
- Added Microsoft 365 Outlook email notifications for both SLA states:
  - `At Risk`
  - `Overdue`
- Added state checks to prevent duplicate notifications during subsequent scheduled evaluator runs.
- The Overdue branch now requires the current SLA Status to be different from `Overdue` before updating the request and sending an escalation.
- The At Risk branch requires the current SLA Status to be different from `At Risk` before updating the request and sending an alert.

### At Risk Validation

Validated the At Risk path using `Test - SLA At Risk Normal` (AR-00020).

Confirmed:

- The Overdue condition evaluated False while the SLA Due Date was still in the future.
- The At Risk condition evaluated True after the SLA At Risk Date passed.
- SharePoint `Update item` completed successfully.
- SLA Status changed to `At Risk`.
- Microsoft 365 Outlook `Send an email (V2)` completed successfully.
- The SLA At Risk alert was delivered to the Outlook inbox.

### Overdue Validation

After the SLA Due Date passed, confirmed:

- The Overdue condition evaluated True.
- SharePoint updated the request to `Overdue`.
- The Outlook escalation action completed successfully.
- The SLA Overdue escalation email was delivered to the Outlook inbox.
- The escalation included the Request ID, request title, priority, SLA status, At Risk Date, and Due Date.

### Duplicate Notification Suppression

Ran the evaluator again after the requests had already reached their SLA states.

Confirmed:

- Requests already marked `Overdue` did not enter the Overdue update/notification branch again.
- Requests already marked `At Risk` do not re-enter the At Risk update/notification branch while remaining in that state.
- Update and email actions were skipped when the request was already in the corresponding SLA state.
- No additional duplicate SLA emails were generated during the validation run.

### Result

The Enterprise Operations Hub SLA evaluator now supports state-aware SLA automation:

`Within SLA -> At Risk -> Overdue`

The evaluator can automatically update SharePoint request state, send Microsoft 365 Outlook notifications when SLA thresholds are crossed, and suppress repeated notifications on subsequent scheduled evaluations.

### Follow-up

- Format SLA timestamps into user-friendly local date/time values in notification emails.
- Continue V2 reporting, metrics, testing, and documentation work.


## 2026-10-08 — V2 SLA Completion Automation Validated

### Completed
- Successfully tested the Access Request - Complete SLA flow.
- Created test request: Test - SLA Completion Before Deadline.
- SharePoint Item ID: 22.
- Confirmed SLA initialization assigned the Normal priority policy.
- Verified SLA Due Date: 2026-10-10T04:22:47Z.
- Verified SLA At Risk Date: 2026-10-09T16:22:47Z.
- Changed request Status to Completed.
- Confirmed Completed Date was automatically populated.
- Confirmed SLA Status automatically changed from Within SLA to Met.
- Verified completion occurred before the SLA deadline.

### V2 SLA Lifecycle
- Within SLA: Initial monitoring state.
- At Risk: Approaching the SLA deadline.
- Overdue: SLA deadline exceeded.
- Met: Request completed within the SLA deadline.
- Previously validated transition-based email alerts and duplicate suppression.

### Result
Successfully validated the SLA completion scenario through SharePoint
and Power Automate. All four SLA states have now been demonstrated.

### Next Steps
- Continue V2 reporting and dashboard improvements.
- Improve SLA date formatting in notification emails.
- Expand automated testing and project documentation.

