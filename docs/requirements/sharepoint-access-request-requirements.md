# SharePoint Access / Permission Change Request — V1 Requirements

## 1. Purpose

The SharePoint Access / Permission Change Request process provides employees with a structured method for requesting access to SharePoint resources or requesting changes to their existing permissions.

The process will replace informal access requests such as email or chat messages with a standardized request, approval, fulfillment, and tracking workflow.

---

## 2. Business Problem

Employees may need access to SharePoint sites, libraries, or other resources to perform their job responsibilities.

Informal access requests can create problems including:

- Missing business justification
- Incorrect permission levels
- Requests being overlooked
- Unclear approval authority
- Limited tracking
- Limited audit history
- Excessive permissions
- Difficulty determining why access was originally granted

The Enterprise Operations Hub will provide a centralized process for managing these requests.

---

## 3. V1 Objective

The first version must allow an employee to:

1. Submit a SharePoint access or permission-change request.
2. Identify the SharePoint resource involved.
3. Specify the requested access.
4. Provide a business justification.
5. Submit the request for approval.
6. Track the status of the request.
7. Receive notification when the request is approved or rejected.

The system must allow the appropriate approver or administrator to review and process the request.

---

## 4. Request Types

V1 will support the following request types:

- New Access
- Change Existing Access
- Remove Access

### New Access

The user currently does not have the required access and is requesting permission to a SharePoint resource.

### Change Existing Access

The user already has access but requires a different permission level.

### Remove Access

Existing access should be removed.

This may eventually support employee transfers, role changes, temporary access expiration, or other identity-lifecycle processes.

---

## 5. Required Request Information

Each request should capture the following information:

### Requester

The employee submitting the request.

Where practical, this information should be obtained automatically from the authenticated Microsoft 365 user rather than requiring the employee to manually type their identity.

### Request Type

One of:

- New Access
- Change Existing Access
- Remove Access

### Target User

The person whose access is being requested or modified.

For V1, the requester may be requesting access for themselves.

The design should allow future expansion for authorized users to submit requests on behalf of another employee.

### SharePoint Resource

The SharePoint resource for which access is requested.

Examples may include:

- SharePoint site
- Document library
- List

V1 should prioritize site-level access before introducing unnecessary permission complexity.

### Requested Permission Level

The requester must select the level of access required to perform their job responsibilities.

Initial standard request options will include:

- Read
- Contribute
- Edit, where specifically justified by the resource and business requirement

**Owner / Full Control will not be available through the standard user access-request process.**

Elevated administrative permissions must be handled through a separate controlled process with additional authorization and auditing.

The solution will follow the principle of least privilege: users should receive only the minimum level of access required to perform their responsibilities.

Where possible, permissions should be granted through approved security or SharePoint groups rather than directly to individual users.

The requested level of access.

Initial options may include:

- Read
- Edit
- Owner / Full Control

Owner or Full Control access should be treated as higher risk than normal Read or Edit access.

### Elevated Access

Owner / Full Control access is considered privileged access and will not be granted through the standard SharePoint access-request workflow.

Administrative or elevated access must follow a separately controlled process with appropriate justification, authorization, and audit history.

This prevents routine users from obtaining permissions that could allow them to alter site configuration, permissions, structure, or other administrative settings.

The access-request system should maintain a traceable record showing who requested access, what resource was requested, the requested permission level, the business justification, who approved the request, and how the request was fulfilled.

### Business Justification

The requester must explain why the access is required.

The justification should provide enough information for an approver to make an informed decision.

### Additional Comments

Optional information that may help the approver or administrator process the request.

---

## 6. System-Generated Information

The system should automatically maintain information including:

- Request ID
- Submission date
- Request status
- Requester identity
- Approval information
- Approval date
- Fulfillment information
- Completion date
- Relevant workflow history

Users should not be responsible for manually entering system-generated tracking information.

---

## 7. Request Status

V1 should support a controlled request lifecycle.

Initial statuses:

```text
Draft
Submitted
Pending Approval
Approved
Rejected
In Progress
Completed
Cancelled
```
