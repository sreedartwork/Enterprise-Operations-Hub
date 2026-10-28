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
