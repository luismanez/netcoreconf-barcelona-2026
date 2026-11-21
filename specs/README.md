# Package Sorting Demo implementation plan

Start with the [global specification](global.md) for the agreed behavior. The [implementation plan](tasks/plan.md) gives the build order, and the [task checklist](tasks/todo.md) records progress. Each feature has its own specification and task list. The scope is the local community demo, its stage data, and the presenter runbook. Verification consists of the frontend and backend build and a live browser rehearsal.

The .NET 10 ASP.NET Core host serves the static React and TypeScript interface and exposes the batch endpoints through Minimal APIs. Server-Sent Events deliver live results to the interface.

## Feature map

| Feature | Responsibility | Depends on | Documents |
| --- | --- | --- | --- |
| Package intake | Photo drop, package IDs, manifest notes, previews, and intake errors | — | [Spec](package-intake/spec.md) · [Tasks](package-intake/tasks.md) |
| Foundry decisions | Multimodal System One request, typed results, raw response, and HTTP duration | Package intake | [Spec](foundry-decisions/spec.md) · [Tasks](foundry-decisions/tasks.md) |
| Batch processing | Routing policy, bounded processing, run state, and live events | Package intake, Foundry decisions | [Spec](batch-processing/spec.md) · [Tasks](batch-processing/tasks.md) |
| Conveyor experience | Projection view, animated lanes, package details, and threshold replay | Batch processing | [Spec](conveyor-experience/spec.md) · [Tasks](conveyor-experience/tasks.md) |
| Live telemetry | Backend measurements, global scoreboard, and technical log | Batch processing, conveyor experience | [Spec](live-telemetry/spec.md) · [Tasks](live-telemetry/tasks.md) |
| Demo readiness | Prepared photo set, presenter runbook, and live rehearsal | All preceding features | [Spec](demo-readiness/spec.md) · [Tasks](demo-readiness/tasks.md) |

The repository documents and planned application copy use English. Paths named in task definitions describe the proposed layout.
