# Demo implementation order

Use the [global specification](../global.md) for the presenter flow and the [feature map](../README.md) for the implementation tasks. Track each task in the [checklist](todo.md). The verification scope is the local build and a browser rehearsal of the presenter flow with the stage photos and configured Foundry deployment.

## Technical approach

- Keep the current batch in a single local ASP.NET Core process. Use .NET 10 Minimal APIs for multipart upload, batch start, the live stream, item details, and threshold changes. Use built-in antiforgery for write requests. The backend reads the JSON manifest and owns the Foundry calls, routing, and clocks.
- Build the single React and TypeScript screen in `ClientApp` with Vite. ASP.NET Core serves the compiled files from `wwwroot/app/` and the API from the same origin.
- Stage with `POST /api/batches`. Open `GET /api/batches/{batchId}/events` and wait for the ready event before sending `POST /api/batches/{batchId}/start`. Use `GET /api/antiforgery` for the request token. The SSE stream delivers package updates, scoreboard snapshots, and the final result to the presenter page. React keys its package state by item ID. [Server-Sent Events in ASP.NET Core](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.typedresults.serversentevents?view=aspnetcore-10.0)

Once the app is scaffolded, run these commands from the repository root and open the ASP.NET Core URL printed by `dotnet run`.

```bash
npm --prefix src/PackageSortingDemo/ClientApp ci
npm --prefix src/PackageSortingDemo/ClientApp run build
dotnet build src/PackageSortingDemo/PackageSortingDemo.csproj
dotnet run --project src/PackageSortingDemo/PackageSortingDemo.csproj
```

## Build order

| Stage | Tasks | Result |
| --- | --- | --- |
| Intake | [ING-01](../package-intake/tasks.md#ing-01), [ING-02](../package-intake/tasks.md#ing-02), [ING-03](../package-intake/tasks.md#ing-03) | The local app stages photos with their operator notes. |
| Live decisions | [DEC-01](../foundry-decisions/tasks.md#dec-01), [RUN-01](../batch-processing/tasks.md#run-01), [RUN-02](../batch-processing/tasks.md#run-02) | Foundry classifies packages and the app streams their results. |
| Conveyor | [UI-01](../conveyor-experience/tasks.md#ui-01), [UI-02](../conveyor-experience/tasks.md#ui-02), [UI-03](../conveyor-experience/tasks.md#ui-03) | The presenter can watch the sorting, inspect the evidence, and show the effect of changing a threshold. |
| Scoreboard | [TEL-01](../live-telemetry/tasks.md#tel-01), [TEL-02](../live-telemetry/tasks.md#tel-02) | The screen shows measured throughput, HTTP latency, and a collapsible log. |
| Stage preparation | [DEM-01](../demo-readiness/tasks.md#dem-01), [DEM-02](../demo-readiness/tasks.md#dem-02) | The presenter has the photo set and a rehearsed script with actual numbers from Foundry. |
