Good. Now we’re ready to define the actual list schema.

This is where we decide, field by field, exactly what SharePoint will store. Paste this entire block into `docs/sharepoint/access-requests-list-design.md`:

````markdown
# Access Requests — SharePoint List Design

## 1. Purpose

This document defines the SharePoint list structure for the Enterprise Operations Hub V1 access-request workflow.

The list will act as the primary request record store for:

- SharePoint access requests
- Permission change requests
- Access removal requests

Each list item will represent one request.

---

# 2. List Name

```text
Access Requests
```
````

---

# 3. Design Principle

The list should store only the information required to:

- identify the requester
- identify the target user
- identify the SharePoint resource
- identify the requested permission level
- capture the business justification
- track approval
- track fulfillment
- preserve an audit trail

Where possible, system-controlled information should be populated automatically rather than manually entered by users.

---

# 4. Column Design

## Request Title

**Display Name:**

```text
Request Title
```

**SharePoint Type:**

```text
Single line of text
```

**Required:** Yes

**Purpose:**

Provides a readable title for the request.

For V1, this may be generated automatically based on the request type and target resource.

Example:

```text
New Access - Finance SharePoint Site
```

The default SharePoint `Title` column may be renamed to `Request Title`.

---

## Request ID

**Display Name:**

```text
Request ID
```

**SharePoint Type:**

```text
Single line of text
```

**Required:** No

**User Editable:** No

**Purpose:**

Provides a human-readable request identifier.

Example:

```text
AR-00001
```

This value should eventually be generated automatically after the SharePoint list item is created.

The built-in SharePoint numeric ID can be used as the source for generating the formatted Request ID.

---

## Requester

**Display Name:**

```text
Requester
```

**SharePoint Type:**

```text
Person or Group
```

**Required:** Yes

**Allow Multiple Selections:** No

**User Editable:** Preferably No

**Purpose:**

Identifies the authenticated employee submitting the request.

The Power Apps form should automatically populate this value using the signed-in Microsoft 365 identity where practical.

---

## Target User

**Display Name:**

```text
Target User
```

**SharePoint Type:**

```text
Person or Group
```

**Required:** Yes

**Allow Multiple Selections:** No

**Purpose:**

Identifies the person whose access will be added, changed, or removed.

For normal self-service requests, the Target User may be the same person as the Requester.

The field exists separately so the system can later support authorized requests submitted on behalf of another employee.

---

## Request Type

**Display Name:**

```text
Request Type
```

**SharePoint Type:**

```text
Choice
```

**Required:** Yes

**Choices:**

```text
New Access
Change Existing Access
Remove Access
```

**Allow Fill-In Choices:** No

**Purpose:**

Identifies the action being requested.

Controlled choices should be used instead of free-text entry so reporting, automation, and validation remain consistent.

---

## SharePoint Resource

**Display Name:**

```text
SharePoint Resource
```

**SharePoint Type:**

```text
Single line of text
```

**Required:** Yes

**Purpose:**

Identifies the SharePoint site or resource involved in the request.

Example:

```text
Finance Department Site
```

V1 will prioritize site-level access.

Future versions may replace this free-text field with a controlled resource catalog.

---

## SharePoint Resource URL

**Display Name:**

```text
SharePoint Resource URL
```

**SharePoint Type:**

```text
Hyperlink
```

**Required:** No

**Purpose:**

Stores the URL of the SharePoint resource involved in the request.

Example:

```text
https://tenant.sharepoint.com/sites/Finance
```

This helps administrators verify that the correct resource is being requested.

---

## Requested Permission

**Display Name:**

```text
Requested Permission
```

**SharePoint Type:**

```text
Choice
```

**Required:** Yes

**Choices:**

```text
Read
Contribute
Edit
```

**Allow Fill-In Choices:** No

**Purpose:**

Identifies the standard permission level being requested.

Owner / Full Control is intentionally excluded from the standard request process.

Elevated access should require a separate privileged-access process.

---

## Business Justification

**Display Name:**

```text
Business Justification
```

**SharePoint Type:**

```text
Multiple lines of text
```

**Required:** Yes

**Purpose:**

Records why the requested access is required.

The justification should provide enough business context for the approver to make an informed decision.

---

## Additional Comments

**Display Name:**

```text
Additional Comments
```

**SharePoint Type:**

```text
Multiple lines of text
```

**Required:** No

**Purpose:**

Allows the requester to provide additional information that may help process the request.

---

## Status

**Display Name:**

```text
Status
```

**SharePoint Type:**

```text
Choice
```

**Required:** Yes

**Default Value:**

```text
Draft
```

**Choices:**

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

**User Editable:** Restricted

**Purpose:**

Tracks the current request lifecycle stage.

Normal requesters should not be able to freely change this field.

Power Automate and authorized administrators should control most status transitions.

---

## Approver

**Display Name:**

```text
Approver
```

**SharePoint Type:**

```text
Person or Group
```

**Required:** No

**Allow Multiple Selections:** No

**Purpose:**

Identifies the person responsible for approving or rejecting the request.

V1 may use a designated approver.

Later versions may determine the approver dynamically based on:

- department
- manager
- SharePoint resource owner
- request type
- data sensitivity

---

## Approval Decision

**Display Name:**

```text
Approval Decision
```

**SharePoint Type:**

```text
Choice
```

**Required:** No

**Choices:**

```text
Pending
Approved
Rejected
```

**User Editable:** Restricted

**Purpose:**

Stores the approval outcome.

This value should be controlled by the approval workflow rather than by the requester.

---

## Approval Comments

**Display Name:**

```text
Approval Comments
```

**SharePoint Type:**

```text
Multiple lines of text
```

**Required:** No

**Purpose:**

Stores comments provided by the approver.

Examples:

```text
Approved for project reporting responsibilities.
```

or:

```text
Rejected because access is not required for the employee's current role.
```

---

## Approval Date

**Display Name:**

```text
Approval Date
```

**SharePoint Type:**

```text
Date and Time
```

**Required:** No

**User Editable:** Restricted

**Purpose:**

Records when the approval decision occurred.

Power Automate should eventually populate this field automatically.

---

## Assigned Administrator

**Display Name:**

```text
Assigned Administrator
```

**SharePoint Type:**

```text
Person or Group
```

**Required:** No

**Allow Multiple Selections:** No

**Purpose:**

Identifies the administrator responsible for fulfilling the approved request.

---

## Fulfillment Notes

**Display Name:**

```text
Fulfillment Notes
```

**SharePoint Type:**

```text
Multiple lines of text
```

**Required:** No

**Purpose:**

Allows the administrator to record how the request was fulfilled.

Example:

```text
User added to Finance Members security group.
Access verified successfully.
```

This field helps preserve technical evidence of fulfillment.

---

## Fulfillment Date

**Display Name:**

```text
Fulfillment Date
```

**SharePoint Type:**

```text
Date and Time
```

**Required:** No

**Purpose:**

Records when the requested technical access change was performed.

---

## Completed Date

**Display Name:**

```text
Completed Date
```

**SharePoint Type:**

```text
Date and Time
```

**Required:** No

**Purpose:**

Records when the request lifecycle was officially completed.

This may be slightly different from Fulfillment Date if verification occurs after the technical access change.

---

## Cancellation Reason

**Display Name:**

```text
Cancellation Reason
```

**SharePoint Type:**

```text
Multiple lines of text
```

**Required:** No

**Purpose:**

Records why a request was cancelled.

---

# 5. Built-In SharePoint Columns

SharePoint automatically provides several system columns.

Examples include:

- ID
- Created
- Created By
- Modified
- Modified By

These built-in columns should be preserved.

They provide useful audit and troubleshooting information.

---

# 6. Request ID Strategy

SharePoint automatically assigns each list item a numeric ID.

Example:

```text
1
2
3
4
```

For the user-facing request identifier, V1 may convert the SharePoint ID into a formatted value.

Example:

```text
ID = 1
```

becomes:

```text
AR-00001
```

The formatted Request ID can be created after the item exists.

---

# 7. Why Request ID Is Not Entered by the User

A requester should not manually type:

```text
AR-00001
```

because this could create:

- duplicate values
- formatting mistakes
- skipped numbers
- inconsistent identifiers

The system should generate the identifier.

---

# 8. User-Controlled vs. System-Controlled Fields

## User-Controlled

The requester may provide:

- Request Type
- Target User
- SharePoint Resource
- SharePoint Resource URL
- Requested Permission
- Business Justification
- Additional Comments

## System-Controlled

The system or authorized personnel should control:

- Request ID
- Requester
- Status
- Approver
- Approval Decision
- Approval Comments
- Approval Date
- Assigned Administrator
- Fulfillment Notes
- Fulfillment Date
- Completed Date

This separation helps prevent users from manipulating workflow or administrative information.

---

# 9. Permission-Level Governance

The standard request process will not offer:

```text
Owner
Full Control
```

as selectable permission levels.

Standard request options are:

```text
Read
Contribute
Edit
```

Even Edit access should only be granted where it is justified by the resource and business requirement.

Privileged access must eventually follow a separate process with additional authorization and auditing.

---

# 10. Validation Requirements

The Power Apps form should eventually validate required information before submission.

Examples:

- Request Type cannot be blank.
- Target User cannot be blank.
- SharePoint Resource cannot be blank.
- Requested Permission cannot be blank for New Access or Change Existing Access.
- Business Justification cannot be blank.
- Remove Access requests may use different permission logic.

Validation should prevent incomplete requests from entering the approval process.

---

# 11. Future Resource Catalog

V1 may initially store the SharePoint resource as text.

A later version may introduce a separate list such as:

```text
SharePoint Resources
```

Possible fields:

- Resource Name
- Site URL
- Business Owner
- Technical Owner
- Department
- Data Classification
- Allowed Permission Levels
- Active / Inactive
- Approval Requirements

This could allow Power Apps to present employees with approved resources rather than allowing arbitrary free-text site names.

This is intentionally deferred from V1.

---

# 12. Future Identity Governance Expansion

The list design should support future capabilities such as:

- automated group membership
- Microsoft Entra integration
- Microsoft Graph provisioning
- PowerShell provisioning
- access expiration
- periodic access reviews
- automatic revocation
- privileged-access requests
- security-control evidence
- compliance reporting

These features will not be implemented until the core request workflow is working.

---

# 13. V1 List Success Criteria

The Access Requests list will be considered correctly designed when it can reliably store:

1. who submitted the request
2. whose access is changing
3. what type of access action is requested
4. which SharePoint resource is involved
5. what permission level is requested
6. why the access is needed
7. the request status
8. who approved or rejected it
9. when the decision occurred
10. who fulfilled the request
11. how the request was fulfilled
12. when the request was completed

The list should support the full lifecycle without allowing normal users to control administrative workflow fields.

````

Then press **⌘ + S**.

A concept worth remembering here is the difference between a **field's display name** and its **data type**.

For example:

```text
Requester
````

is the name humans see.

But:

```text
Person or Group
```

is how SharePoint actually stores and understands that data.

That distinction is going to matter a lot when we start working with Power Apps and Power Automate.

Once this is saved, tell me **saved**.
