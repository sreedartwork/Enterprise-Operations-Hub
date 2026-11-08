# V2-012 — SharePoint Access Requests Security Validation

Date: October 27, 2026
Status: PENDING — Final employee access test

## Verified SharePoint Permissions

List: Enterprise Operations Hub / Access Requests

| Principal | Permission | Status |
|---|---|---|
| Enterprise Operations Hub Owners | Full Control | Verified |
| Enterprise Operations Hub Members | Contribute | Verified |
| Enterprise Operations Hub Visitors | Removed from list permissions | Verified |
| EOH Test Employee | Contribute via Members group | Verified |

The Access Requests list has unique permissions.

## Item-Level Security Configuration

- Read access: Read items created by the user.
- Create/Edit access: Create items and edit items created by the user.
- Both settings verified in SharePoint Advanced Settings.

## Effective Permissions Verification

SharePoint Check Permissions confirmed:

- Account: EOH Test Employee
- Permission level: Contribute
- Granted through: Enterprise Operations Hub Members

## Outstanding Validation

The following tests remain pending:

1. Reset the EOH Test Employee password.
2. Sign in using a separate browser session.
3. Verify the employee can access the Access Requests list.
4. Verify the employee can create a request.
5. Verify the employee cannot read or modify another user's requests.
6. Confirm licensing does not prevent the test.

## Security Notes

- SharePoint item-level restrictions are configured but not yet independently validated.
- Power Apps UI filtering alone does not establish data-layer security.
- The test account may require appropriate Microsoft 365 licensing.
- Do not mark V2-012 PASS until the employee access tests succeed.

## Next Session

Resume with Microsoft Entra password reset and employee access validation.

V2-012 remains PENDING.

---

## November 8, 2026 — Final V2 Portfolio Security Validation Update

**Current status:** PASS within the documented V2 portfolio test scope.

The October 27 findings above are historical and describe the earlier SharePoint permission configuration. They do not represent the final V2 security architecture.

### Updated SharePoint Security Architecture

- `Access Requests - Employee Intake` is the employee-facing submission list with separate permissions and item-level restrictions.
- `Access Requests` is the restricted administrator list with unique permissions.
- Employees are not intended to receive direct access to the administrator list.
- The designated test approver successfully completed an approval through Power Automate Approvals without direct administrator-list access.
- Direct access to the administrator list was denied to the designated test approver.

### Validated Behavior

- Employee intake isolation was validated within the documented test scope.
- Intake-to-administrator transfer was validated.
- Sequential replay testing confirmed duplicate prevention in the tested scenario.
- The V2 regression matrix records 13 PASS, 0 PENDING, and 0 FAIL.

### Remaining Security Limitations

- The updated approval rejection path requires validation.
- Broader multi-account and negative-path testing remains outstanding.
- Simultaneous-request concurrency and duplicate prevention have not been stress-tested.
- Approval routing currently uses a specific assigned test user rather than dynamic group-based routing.
- Actual SharePoint permission grants during fulfillment have not been independently verified.

**Release classification:** Suitable for portfolio demonstration within the documented validation scope. Not validated for production deployment involving sensitive access-request information.

See the V2 regression matrix, V2-012 validation checkpoint, and V2 release readiness checklist for supporting evidence.
