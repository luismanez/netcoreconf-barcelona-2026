# Tasks — Batch processing

Paths are relative to `src/PackageSortingDemo`. Track completion in the [checklist](../tasks/todo.md).

## RUN-01

**Process a staged batch**

Start the batch after intake and record the start time. Process ready items in the local app with bounded concurrency, starting with eight in flight for rehearsal. Record when each item's request starts. Apply the proposed route at or above the threshold and send it to Inspect for human review below the threshold. Use the nearest urgency level for the score's display label, with midpoint values rounded up.

- **Acceptance.** Each ready item gets one call and its own applied route or failure. A second start on a running batch keeps the existing run, and a failed item lets the remaining items continue. The batch finishes with a terminal outcome for every item.
- **Dependencies.** ING-03, DEC-01.
- **Likely files.** `Batches/BatchEndpoints.cs`, `Batches/BatchStore.cs`, `Batches/BatchProcessor.cs`, `Batches/RoutingPolicy.cs`, `appsettings.json`.

## RUN-02

**Send live results to the conveyor**

Expose the batch SSE endpoint. Attach the presenter stream to the current batch, then send a ready event. The page waits for that event before sending the start request. Send package milestones, item summaries, and the final outcome. Keep the raw JSON in the package details.

- **Acceptance.** Results and errors reach the page as processing finishes for each package, and the page receives a completion event after the final item.
- **Dependencies.** RUN-01.
- **Likely files.** `Batches/BatchEvents.cs`, `Batches/BatchEndpoints.cs`, `Batches/BatchProcessor.cs`.
