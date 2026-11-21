# Tasks — Live telemetry

Paths are relative to `src/PackageSortingDemo`. Track completion in the [checklist](../tasks/todo.md).

## TEL-01

**Calculate the live batch figures**

Use the batch clock and stored results to calculate classified count, elapsed-time throughput, p50 and p95 of valid call durations, and upload and processing error counts. Send the figures in the live events and include the final values with completion.

- **Acceptance.** The figures come from backend timings. Human review counts as a classification, failures appear in their own counters, and the final rates use the measured batch duration.
- **Dependencies.** RUN-02.
- **Likely files.** `Telemetry/BatchMetrics.cs`, `Batches/BatchProcessor.cs`, `Batches/BatchEvents.cs`.

## TEL-02

**Show the scoreboard and run log**

Render the scoreboard and a collapsible log in React using the existing live event stream. Keep the three headline figures legible on the projector. Include package IDs, timestamps, durations, and useful failure messages in the log.

- **Acceptance.** The scoreboard updates as the line sorts and keeps the final figures available during the walkthrough. The presenter can open the log during or after the run.
- **Dependencies.** UI-01, TEL-01.
- **Likely files.** `ClientApp/src/App.tsx`, `ClientApp/src/components/BatchScoreboard.tsx`, `ClientApp/src/components/RunLog.tsx`, `ClientApp/src/contracts.ts`, `ClientApp/src/index.css`.
