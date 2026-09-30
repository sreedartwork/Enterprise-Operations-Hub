# Operations Dashboard Metrics Architecture

## Purpose

The Operations Dashboard provides aggregate request metrics without requiring Power Apps to calculate counts directly against the full SharePoint `Access Requests` list.

The dashboard displays:

- Total Requests
- Pending Approval
- Approved
- In Progress
- Completed

## Original Design

The initial Power Apps dashboard calculated metrics directly from the SharePoint `Access Requests` list using formulas such as:

```powerfx
CountRows([@'Access Requests'])
```

This produced Power Apps delegation warnings.

A delegation warning means Power Apps cannot guarantee that the operation will be executed against the complete SharePoint dataset as the list grows. This creates a risk that dashboard values could become incomplete or inaccurate at larger data volumes.

## Why the Architecture Changed

Rather than hiding or ignoring the delegation warnings, dashboard aggregation was moved out of Power Apps.

The revised architecture is:

```text
Access Requests
      |
      | item created or modified
      v
Power Automate
      |
      | calculates request metrics
      v
Request Metrics
      |
      | precomputed values
      v
Power Apps Operations Dashboard
```

This separates two responsibilities:

- Power Automate performs the aggregation.
- Power Apps presents the already-calculated results.

Power Automate calculates the metrics and writes them to the dedicated SharePoint `Request Metrics` list.

Power Apps retrieves those values using formulas such as:

```powerfx
LookUp(
    'Request Metrics',
    Title = "Dashboard Metrics",
    'Total Requests'
)
```

Power Apps therefore no longer needs to count the operational `Access Requests` list directly.

## Dashboard Refresh

`OperationsDashboardScreen.OnVisible` contains:

```powerfx
Refresh('Request Metrics')
```

This causes Power Apps to retrieve the latest metrics whenever the Operations Dashboard becomes visible instead of relying on an older cached copy.

## Current 5,000-Item Aggregation Boundary

The Power Automate `Get Total Requests` action uses pagination with a threshold of 5,000 records.

Pagination tells Power Automate to continue retrieving additional pages of SharePoint results rather than relying on only the initial batch.

The 5,000-item threshold is a documented boundary of the current V2 implementation. It is not a claim that the architecture has unlimited scalability.

## Why Not Simply Keep Increasing the Threshold?

Increasing the pagination threshold may allow Power Automate to retrieve more records where supported.

However, the larger architectural question is not simply:

> How high can the pagination threshold be set?

The more important question is:

> Should every request update require retrieving thousands of historical requests just to recalculate dashboard totals?

At substantially larger data volumes, repeatedly retrieving the complete historical request dataset simply to calculate a few aggregate values becomes increasingly inefficient.

Therefore, continually increasing the pagination threshold would not necessarily be the preferred long-term scaling strategy.

## Future Scaling Option: Incremental Metrics

A future implementation could maintain metrics incrementally rather than recounting the complete request dataset.

For example, if a request changes from:

```text
Approved -> In Progress
```

the system could conceptually perform:

```text
Approved:    43 -> 42
In Progress: 28 -> 29
```

rather than retrieving every request and counting each status again.

Similarly, creation of a new request could increment:

```text
Total Requests: 50000 -> 50001
```

This is similar to a scoreboard. When a team scores, the scoreboard updates the existing score instead of reviewing every previous scoring play and recalculating the score from the beginning.

## Incremental Counter Tradeoffs

Incremental metrics would be more efficient at high volume, but they introduce additional consistency requirements.

Potential concerns include:

- duplicate flow execution
- failed or partially completed flows
- concurrent request updates
- counters drifting from the authoritative request data

A more mature implementation could therefore require:

- idempotency controls
- concurrency handling
- error recovery
- periodic reconciliation against the authoritative `Access Requests` dataset

This additional complexity is not currently necessary for the V2 portfolio implementation.

## Future Data and Reporting Architecture

If request volume, reporting complexity, governance requirements, or integration requirements grow substantially, the solution should also reconsider whether SharePoint remains the appropriate aggregation and analytics platform.

Depending on future requirements, technologies that could be evaluated include:

- Dataverse
- Power BI
- Azure-based processing or data services
- another dedicated reporting or analytics layer

These technologies should be introduced only when justified by actual requirements rather than added solely for architectural complexity.

## Current Design Principle

The V2 implementation favors an architecture that is simple enough to validate while explicitly documenting its scaling boundary.

The goal is not to claim unlimited enterprise scale.

The goal is to understand:

1. where the current architecture works,
2. where its limitations begin,
3. why those limitations exist, and
4. which architectural decisions should be reconsidered as requirements grow.
