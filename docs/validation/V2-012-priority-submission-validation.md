# V2-012 — Priority Submission Validation

Date: 2026-10-25

## Confirmed
- Added the required Priority field to the Power Apps Access Requests form.
- Configured new requests to default Priority to Normal.
- Moved Priority into the visible form layout.
- Successfully submitted the test request "V2-012 - Priority Submission Test".
- Confirmed the saved record displays Priority = Normal in Power Apps.
- Independently verified Priority = Normal in the SharePoint Access Requests list.
- Verified the request was created with Status = Draft.

## Still pending
- SharePoint list-level least-privilege security validation.
- Remove the temporary diagnostic label from the app.
- Final review and publication of the app.

## Result
Priority submission and SharePoint persistence: PASS.
V2-012 overall security validation: PENDING.

---

## November 8, 2026 — Validation Status Update

**Current V2-012 status:** PASS within the documented V2 portfolio test scope.

The October 25 pending items above reflect the project's status at that time and are preserved as historical validation evidence.

Subsequent V2 testing validated employee intake isolation, intake-to-administrator transfer, sequential duplicate prevention, and designated approver role separation.

The V2 regression matrix now records 13 PASS, 0 PENDING, and 0 FAIL.

The final V2 architecture uses a separate employee-facing intake list and a restricted administrator Access Requests list.

**Outstanding limitations:** Updated approval rejection testing, broader negative-path security validation, simultaneous-request concurrency testing, and independent verification of fulfillment permission grants remain future work.

**Release classification:** Portfolio demonstration ready within documented test scope; not validated for production deployment.

See the V2 regression test matrix and V2 release readiness checklist for the current validation evidence.
