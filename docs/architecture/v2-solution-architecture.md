# Enterprise Operations Hub — V2 Solution Architecture

## 1. Purpose

V2 extends the SharePoint access-request solution with SLA management, operational reporting, notifications, and activity tracking.

This document describes implemented and documented capabilities, not a proposed production deployment.

## 2. Technology Stack

- SharePoint Online
- Power Apps
- Power Automate
- Microsoft 365 identities and group-based application role awareness

## 3. SharePoint Data Architecture

| List | Responsibility |
|---|---|
| Access Requests | Request lifecycle, approvals, fulfillment, and SLA fields |
| Request Activity | Records relevant request status changes |
| Request Metrics | Stores aggregated dashboard metrics |
| SLA Policies | Stores priority-based SLA targets |

## 4. Request Lifecycle

Employee submission through Power Apps creates a SharePoint request.

Power Automate supports approval and rejection processing.

Approved requests can proceed through administrator assignment, manual fulfillment recording, and completion.

Approval authorizes the requested work; fulfillment records its execution.

Actual SharePoint permission grants were not independently verified in the documented fulfillment tests.

## 5. SLA Architecture

Four policies define calendar-elapsed SLA targets:

- Critical: 1 hour
- High: 4 hours
- Normal: 2 days
- Low: 5 days

Power Automate workflows initialize SLA dates, recalculate relevant changes, evaluate At Risk and Overdue conditions, and record completion outcomes.

Documented testing also verified notification delivery and suppression of repeated processing in specific scenarios.

## 6. Operations Dashboard

The published SharePoint homepage displays six metrics:

- Total Requests
- Pending Approval
- Approved
- In Progress
- Completed
- Overdue

Data flow:

Access Requests -> Power Automate -> Request Metrics -> SharePoint homepage list web part

Metrics are precomputed to avoid direct Power Apps aggregation delegation issues.

The current total-request aggregation has a documented 5,000-item pagination boundary.

See [Dashboard Metrics Architecture](dashboard-metrics-architecture.md).

## 7. Activity Tracking

Relevant request status transitions generate records in Request Activity.

Documented tests confirmed that unrelated field changes did not create unnecessary status-change events.

This is application-level activity tracking, not a claim of comprehensive Microsoft 365 audit coverage.

## 8. Security Boundary

Power Apps provides role-aware requester and administrator interfaces.

SharePoint data-layer item-level permissions have not been fully implemented or verified.

Application-level filtering does not replace SharePoint authorization.

V2 is a portfolio/development demonstration and must not be considered production-ready for sensitive access-request information.

## 9. Validation

The V2 regression matrix records:

- 12 PASS
- 1 PENDING
- 0 FAIL

V2-012 remains pending for SharePoint data-layer permission enforcement and verification.

Testing covers documented scenarios, not exhaustive production, concurrency, or scalability validation.

See [V2 Regression Test Matrix](../testing/V2_REGRESSION_TEST_MATRIX.md).

## 10. Future Enhancements

Potential V3 work includes stronger data-layer security, advanced concurrency handling, improved monitoring, scalable reporting, graphical KPI cards, and deployment automation.
