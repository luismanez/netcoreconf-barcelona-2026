# Tasks — Conveyor experience

Paths are relative to `src/PackageSortingDemo`. Track completion in the [checklist](../tasks/todo.md).

## UI-01

**Animate the live conveyor**

Connect the React screen to the start endpoint and SSE stream. Keep package state keyed by item ID and animate each completed result into Continue, Repack, or Inspect as it arrives. Show urgency with color and a label, and mark human review. Close the stream when the run completes or the connection fails, and show a clear status for an interruption.

- **Acceptance.** The presenter can start a staged batch and watch it sort on the projection screen. Out-of-order responses move the correct photos. Failed items and lost connections are visible.
- **Dependencies.** RUN-02.
- **Likely files.** `ClientApp/src/App.tsx`, `ClientApp/src/components/Conveyor.tsx`, `ClientApp/src/useBatchEvents.ts`, `ClientApp/src/contracts.ts`, `ClientApp/src/components/conveyor.css`.

## UI-02

**Open a package's decision details**

Expose item details by batch and item ID. Open a React drawer from the selected package and show the photo, note, model answers, all route probabilities, proposed and applied route, human-review reason, raw JSON, and queue and HTTP timings. Show the reason and available diagnostics for a failed item.

- **Acceptance.** The presenter can select a finished or failed item and see its own evidence and diagnostics.
- **Dependencies.** UI-01.
- **Likely files.** `Batches/BatchEndpoints.cs`, `ClientApp/src/components/PackageDetails.tsx`, `ClientApp/src/App.tsx`, `ClientApp/src/api.ts`, `ClientApp/src/contracts.ts`.

## UI-03

**Show the effect of a different threshold**

Add a threshold control to the detail panel and rerun the existing routing policy on the saved answer for that item. Apply the resulting route to the conveyor and show the human-review badge when appropriate.

- **Acceptance.** An already classified package can move to human review using its existing answer. Its raw response and the measured batch statistics are carried over from the original run.
- **Dependencies.** UI-02.
- **Likely files.** `Batches/BatchEndpoints.cs`, `Batches/BatchStore.cs`, `ClientApp/src/components/PackageDetails.tsx`, `ClientApp/src/App.tsx`, `ClientApp/src/api.ts`.
