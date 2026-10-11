# Enterprise Operations Hub — V2 Operations Dashboard Requirements

## Purpose

V2 expands the completed V1 request-management workflow into an operational management experience.

The first V2 capability will be an Operations Dashboard that gives authorized administrators visibility into the overall SharePoint access-request workload without requiring them to review individual requests one at a time.

## V2 Dashboard Objectives

The dashboard should allow an authorized administrator to quickly understand:

- Total number of requests
- Requests pending approval
- Approved requests awaiting fulfillment
- Requests currently in progress
- Completed requests
- Recent request activity

## Initial Functional Requirements

### 1. Administrator Access

The Operations Dashboard should be available only through the administrator experience already established in V1.

### 2. Request Metrics

The dashboard should calculate request counts from the existing SharePoint `Access Requests` data source.

Initial metrics:

- Total Requests
- Pending Approval
- Approved
- In Progress
- Completed

### 3. Operational Visibility

Administrators should be able to identify requests requiring attention without manually reviewing the entire SharePoint list.

### 4. Existing V1 Data

The first dashboard implementation should use the existing V1 SharePoint request data rather than introducing a new data platform.

### 5. Future Expansion

The dashboard should be designed so later V2 capabilities can add:

- SLA and overdue-request indicators
- Additional filtering
- Recent activity
- Notifications
- Reporting and Power BI integration
- Additional request-management metrics

## V2 Design Principle

V1 focuses on processing individual requests.

V2 begins expanding the solution toward operational management by providing visibility into the overall request workload.
