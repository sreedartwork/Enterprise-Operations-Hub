# Learning Notes — Dashboard Metrics, Delegation, and Scalability

## What Problem Did I Run Into?

The Operations Dashboard originally calculated request totals directly in Power Apps.

For example:

```powerfx
CountRows([@'Access Requests'])
```

This worked with the small test dataset, but Power Apps displayed delegation warnings.

The important lesson is that a formula working with 10 records does not necessarily mean it will continue producing reliable results when the SharePoint list contains thousands of records.

## What Is Delegation?

Delegation means Power Apps can send an operation to the underlying data source and allow that system to perform the work against the full dataset.

In simple terms:

```text
Delegated:
Power Apps -> "SharePoint, calculate this against your data."

Potentially non-delegated:
Power Apps -> retrieves a limited set of records -> calculates locally
```

A delegation warning therefore matters because Power Apps may not evaluate the complete dataset.

For an operational dashboard, potentially incomplete counts are not acceptable.

## Why Did I Change the Architecture?

I could have ignored the yellow warnings because everything appeared correct with the small test dataset.

Instead, I treated the warning as an architectural issue.

Originally:

```text
Access Requests
      |
      v
Power Apps
      |
      v
Count the records
      |
      v
Display dashboard
```

The revised design is:

```text
Access Requests
      |
      | created or modified
      v
Power Automate
      |
      | calculate metrics
      v
Request Metrics
      |
      | store aggregate values
      v
Power Apps Dashboard
```

Power Apps is now responsible primarily for presentation.

Power Automate performs the aggregation, and SharePoint stores the resulting metrics.

Power Apps retrieves a precomputed value using formulas such as:

```powerfx
LookUp(
    'Request Metrics',
    Title = "Dashboard Metrics",
    'Total Requests'
)
```

This eliminated the dashboard delegation warnings.

## Why Refresh Request Metrics?

Power Apps can retain previously retrieved data.

The dashboard therefore uses:

```powerfx
Refresh('Request Metrics')
```

in:

```text
OperationsDashboardScreen.OnVisible
```

In plain English:

> Every time the dashboard becomes visible, retrieve the latest Request Metrics values from SharePoint.

This was tested by changing an Access Request status, verifying that Power Automate updated Request Metrics, and then reopening the dashboard.

The new values appeared after the screen became visible.

## What Does the 5,000 Pagination Threshold Mean?

The `Get Total Requests` Power Automate action retrieves the Access Requests used to calculate the total.

Pagination was enabled with a threshold of 5,000.

The basic idea is:

> If the results require multiple pages, continue retrieving additional pages up to the configured threshold.

This makes the current implementation safer for a larger dataset than relying on only an initial batch of records.

However, 5,000 is a documented boundary of the current implementation.

It does NOT mean the architecture scales infinitely.

## Couldn't I Just Increase 5,000?

Possibly, where supported.

If the list grew beyond the current boundary, increasing the pagination threshold could be one short-term option.

But this is where the engineering question changes.

The question should not only be:

> Can I change 5,000 to a larger number?

The better question is:

> Should I retrieve thousands of historical records every time one request changes just to calculate a few dashboard numbers?

For example, imagine there are 50,000 historical Access Requests.

One request changes:

```text
Approved -> In Progress
```

Re-reading tens of thousands of historical records just to discover the new totals would become increasingly inefficient.

Therefore, simply making the pagination number larger is not necessarily the best long-term architecture.

## The Scoreboard Analogy

Think about a basketball scoreboard.

Suppose the score is:

```text
84
```

A player makes a three-point shot.

The scoreboard does not replay the entire game and recount every previous basket.

It performs:

```text
84 + 3 = 87
```

A high-volume request metrics system could eventually work similarly.

Suppose:

```text
Approved    = 43
In Progress = 28
```

A request changes:

```text
Approved -> In Progress
```

Instead of recounting every historical request, the system could conceptually perform:

```text
Approved:    43 -> 42
In Progress: 28 -> 29
```

A newly created request could similarly perform:

```text
Total Requests: 50000 -> 50001
```

This is an incremental metrics architecture.

## Why Didn't I Build Incremental Metrics Now?

Because greater scalability can introduce greater complexity.

Incremental counters create new problems that must be handled correctly.

Examples include:

- What if the flow runs twice?
- What if the flow fails after decrementing one counter but before incrementing another?
- What if two requests update simultaneously?
- What if the metrics counters drift away from the real Access Requests data?

A more mature incremental architecture may therefore require:

- idempotency controls
- concurrency controls
- error handling and recovery
- periodic reconciliation against the authoritative dataset

For the current V2 implementation, recounting the source data within a documented boundary is simpler to understand, test, and validate.

The important engineering lesson is:

> Do not add complexity before the requirements justify it.

## What Would I Reconsider As Data Volume Grows?

As volume increases, I would reconsider several things.

### 1. Aggregation Strategy

Instead of recalculating metrics from the complete request dataset, evaluate incremental metric updates.

### 2. Reconciliation

If incremental counters are introduced, periodically compare them with the authoritative request dataset to detect and repair drift.

### 3. Data Platform

If volume, reporting, governance, or integration requirements become substantially more complex, reconsider whether SharePoint should continue serving all of these responsibilities.

Depending on actual requirements, technologies worth evaluating could include:

- Dataverse
- Power BI
- Azure-based processing or data services
- another dedicated analytics or reporting layer

The decision should be driven by requirements, not by adding technology merely to make the architecture look more complicated.

## What Did I Actually Test?

The implementation was tested end-to-end.

One test changed:

```text
Pending Approval -> Approved
```

The expected metrics were predicted before the test.

Power Automate updated Request Metrics correctly.

A second test changed:

```text
Approved -> In Progress
```

The resulting Request Metrics values were verified as:

```text
Total Requests   = 10
Pending Approval = 0
Approved         = 0
In Progress      = 1
Completed        = 2
```

Power Apps was also verified to retrieve the updated metrics after `OperationsDashboardScreen` became visible.

This demonstrated:

```text
Access Requests
      ->
Power Automate
      ->
Request Metrics
      ->
Power Apps Operations Dashboard
```

## How I Can Explain This in an Interview

A concise explanation:

> Initially, the Operations Dashboard calculated metrics directly against the SharePoint Access Requests list in Power Apps. During development I encountered delegation warnings, which meant those calculations were not a reliable foundation as the dataset grew. Instead of ignoring the warnings, I moved the aggregation into Power Automate and created a Request Metrics list containing precomputed dashboard values. Power Apps now reads those metrics rather than counting the operational list itself.
>
> I also configured pagination for the total-request retrieval and documented a 5,000-item boundary for the current implementation. If request volume grew substantially, I would not simply keep increasing that threshold indefinitely. I would reevaluate the aggregation strategy, potentially using incremental metrics or moving reporting and analytics responsibilities to a more appropriate data platform.

## Key Concepts I Should Remember

**Delegation**
Power Apps asks the data source to perform an operation against the complete dataset.

**Aggregation**
Turning many individual records into summary information such as totals and status counts.

**Pagination**
Retrieving a large result set in multiple pages/batches rather than assuming everything arrives in one response.

**Precomputed Metric**
A metric calculated ahead of time and stored so the UI can retrieve the result instead of recalculating it.

**Incremental Metric**
Updating an existing aggregate based on what changed rather than recalculating the aggregate from the complete dataset.

**Idempotency**
Designing an operation so repeating the same event does not incorrectly apply the same change multiple times.

**Concurrency**
Handling multiple operations that may occur at or near the same time without corrupting data.

**Reconciliation**
Periodically comparing calculated/stored metrics against the authoritative source data to detect and correct differences.

## Main Lesson

The important part of this work was not simply removing yellow Power Apps warnings or setting pagination to 5,000.

The important part was learning to recognize a scaling limitation, change the responsibilities of the system appropriately, test the revised architecture end-to-end, document its current boundary, and understand what should be reconsidered when the requirements become larger.
