# Enterprise Operations Hub — V3 Development Roadmap

**Branch:** `v3-development`  
**Status:** Planning  
**Previous milestone:** V2 Portfolio Checkpoint

## Mission

Evolve the Enterprise Operations Hub from a working SharePoint and Power Platform portfolio application into a more secure, maintainable, measurable, and reusable enterprise operations solution.

## Phase 0 — Complete V2 Validation

**Priority:** Critical  
**Status:** Pending

- [ ] V2-012: Verify SharePoint data-layer security using separate employee and administrator accounts.
- [ ] Confirm employees cannot access unauthorized requests through SharePoint directly.
- [ ] Verify that application UI filtering is not being mistaken for backend authorization.
- [ ] Run a fresh approval-to-fulfillment regression test.
- [ ] Record evidence, limitations, and test results.

**Exit criteria:** Security findings are documented, required fixes are completed, and regression tests pass. Do not claim production readiness before validation.

## Phase 1 — Architecture and Security

**Status:** Planned

- [ ] Review SharePoint lists, columns, relationships, and permissions.
- [ ] Document user roles and authorization boundaries.
- [ ] Evaluate SharePoint versus Dataverse for future scale and security needs.
- [ ] Create an architecture diagram and decision log.
- [ ] Define nonfunctional requirements and acceptance criteria.

**Exit criteria:** Documented architecture, threat considerations, and approved implementation scope.

## Phase 2 — Workflow Reliability

**Status:** Planned

- [ ] Review Power Automate error handling and retry behavior.
- [ ] Evaluate duplicate events and concurrent updates.
- [ ] Improve operational logging and failure visibility.
- [ ] Validate SLA calculations and status transitions.
- [ ] Add repeatable workflow test cases.

**Exit criteria:** Tested workflows with documented failure handling and recovery procedures.

## Phase 3 — Administration and Reporting

**Status:** Planned

- [ ] Improve administrator workflows and request visibility.
- [ ] Define meaningful operational KPIs.
- [ ] Validate dashboard metrics against source records.
- [ ] Evaluate reporting options, including Power BI where licensing permits.
- [ ] Document reporting limitations and data refresh behavior.

**Exit criteria:** Accurate reporting with reproducible verification steps.

## Phase 4 — Engineering and Deployment

**Status:** Planned

- [ ] Introduce PowerShell or PnP PowerShell for appropriate administrative tasks.
- [ ] Evaluate Microsoft Graph and Entra ID integration needs.
- [ ] Document environment strategy and configuration management.
- [ ] Explore Power Platform solutions and application lifecycle management.
- [ ] Define a repeatable deployment and rollback process.

**Exit criteria:** Documented, tested deployment procedures and maintainable configuration.

## Phase 5 — Portfolio and Commercial Readiness

**Status:** Planned

- [ ] Update README and technical architecture documentation.
- [ ] Capture demonstrations and evidence of completed functionality.
- [ ] Prepare a technical case study with measurable outcomes.
- [ ] Identify a narrowly scoped, reusable implementation offering.
- [ ] Assess licensing, support, maintenance, and security responsibilities.
- [ ] Update portfolio and LinkedIn only with verified capabilities.

**Exit criteria:** Clear technical documentation, credible demonstration, and a defined potential service offering.

## Learning Progression

For each major feature, follow:

**BUILD → UNDERSTAND → CHANGE → TROUBLESHOOT → EXPLAIN → DESIGN → MONETIZE**

Maintain formula explanations, troubleshooting notes, architectural decisions, and interview-ready examples.

## Current Next Action

Complete **V2-012 SharePoint data-layer security validation** before beginning major V3 feature development.

## Change Log

- 2026-10-15 — Initial V3 roadmap drafted. Phases are proposed and subject to review.

## October 19, 2026 — V3 Security Validation

**Branch:** `v3-development`
**Task:** V2-012 — SharePoint Data-Layer Security
**Status:** IN PROGRESS

### Work Completed

- Reviewed SharePoint permissions for the Access Requests list.
- Confirmed the list inherits permissions from the parent site.
- Reviewed Owners, Members, and Visitors groups.
- Created an unlicensed test employee account.
- Confirmed the test account currently has no Access Requests list permissions.
- Inspected Power Apps Requester field configuration.

### Security Findings

- Requester defaults to the signed-in user when creating a request.
- Requester selection is searchable.
- The form submits the selected Requester value.
- No explicit application-level restriction was found preventing Requester changes.
- SharePoint item-level settings currently allow users with sufficient list permissions to read and edit all items.

### Next Steps

1. Set `DataCardValue3.DisplayMode` to `DisplayMode.View`.
2. Test Requester behavior in new and existing requests.
3. Review SharePoint authorization and item-level access.
4. Validate using a properly licensed employee identity when available.
5. Document security findings and rerun regression tests.

### Validation Status

**V2-012 remains PENDING.**

The application is a portfolio demonstration and has not been validated as production-ready.
