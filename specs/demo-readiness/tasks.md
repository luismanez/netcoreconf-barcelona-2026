# Tasks — Demo readiness

Paths are relative to the repository root. Track completion in the [checklist](../tasks/todo.md).

## DEM-01

**Prepare the stage photos and notes**

Prepare roughly 48–60 labelled PNG or JPEG files and add their notes to the manifest. Include examples for all three lanes, several urgency levels, and two IDs for the same photo with different notes. Set aside candidates for the threshold demonstration.

- **Acceptance.** Each stage photo has a matching note and the set supports the presenter walkthrough.
- **Dependencies.** ING-03.
- **Likely files.** `assets/demo-packages/`, `src/PackageSortingDemo/Data/packages.json`.

## DEM-02

**Write the runbook and rehearse the stage flow**

Write a short runbook with local startup, Foundry settings, the raw multimodal request, the single-package walkthrough, and the batch run with the details and threshold change. Include the endpoint and model distinction for the OpenAI comparison slide. Build both projects and rehearse this flow from the local web app using the stage deployment and photos. Choose the batch size, concurrency, contrast pair, and threshold example from the rehearsal.

- **Acceptance.** The presenter can follow the runbook from startup through the final scoreboard and repeat the threshold demonstration. The runbook records the actual latency, throughput, and error count or the specific blocker for a live run.
- **Dependencies.** UI-03, TEL-02, DEM-01.
- **Likely files.** `docs/demo-runbook.md`, `specs/tasks/todo.md`, `src/PackageSortingDemo/appsettings.json` if rehearsal changes the in-flight limit.
