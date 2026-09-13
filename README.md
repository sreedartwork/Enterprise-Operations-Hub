# Enterprise Operations Hub

An enterprise-style Microsoft 365 operations and request management solution built as a professional portfolio project.

The Enterprise Operations Hub demonstrates how Microsoft 365 administration, SharePoint Online, Power Platform, automation, reporting, scripting, and Microsoft Graph can be combined to support realistic enterprise business processes.

## Project Objective

The goal of this project is to demonstrate the transition from Microsoft 365 / SharePoint administration into Microsoft 365 and Power Platform development.

The solution is designed around a fictional enterprise organization of approximately 3,500 employees.

Employees will use the platform to submit operational and IT requests. Managers can review and approve requests, IT teams can fulfill them, administrators can manage the platform, and leadership can review operational reporting.

## Core Business Process

The planned workflow is:

Employee  
↓  
SharePoint Online Portal  
↓  
Power Apps Request Interface  
↓  
SharePoint Lists / Dataverse  
↓  
Power Automate Workflow  
↓  
Manager / IT Approval  
↓  
Microsoft 365 / Entra ID  
↓  
Reporting, Auditing, and Governance

## V1 Goal

The first working version will focus on an end-to-end:

**SharePoint Access / Permission Change Request**

A user will be able to:

1. Access the Enterprise Operations Hub.
2. Submit a SharePoint permission request.
3. Provide the required request information.
4. Send the request into an approval workflow.
5. Allow the appropriate manager or administrator to approve or reject it.
6. Track the request status.
7. Receive workflow notifications.
8. Maintain a record of the request for auditing and reporting.

The V1 milestone is:

> **SharePoint Online + Power Apps + Power Automate working end-to-end.**

## Planned Technology Stack

### Microsoft 365

- SharePoint Online
- Microsoft Teams
- Microsoft Entra ID
- Microsoft Graph

### Power Platform

- Power Apps
- Power Automate
- Dataverse
- Power BI

### Administration & Automation

- PowerShell
- PnP PowerShell
- Microsoft Graph API

### Future Expansion

- C#
- ASP.NET Core Web API
- Microsoft Azure

The future technologies will be added only after the core Microsoft 365 and Power Platform solution is working.

## Planned SharePoint Portal

The Enterprise Operations Hub portal is planned to include:

- Home
- Submit Request
- My Requests
- Knowledge Base
- Policies
- Reports
- Administration

The SharePoint implementation will demonstrate enterprise concepts including information architecture, permissions, metadata, content types, navigation, search, governance, and lifecycle management.

## Repository Structure

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
