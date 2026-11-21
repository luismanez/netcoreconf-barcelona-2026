# Feature — Live telemetry

The scoreboard and log use backend measurements and run events. The batch clock starts when live processing begins after intake and ends when every submitted item has an applied route or a recorded failure. Each Foundry HTTP timing covers request send through complete response-body receipt. Queue wait is available as a separate duration for an item.

| Scoreboard value | Definition |
| --- | --- |
| **Packages classified / total** | Items with a valid model result and applied route, including human review, over all submitted photos. Intake and processing error counts provide the rest of the context. |
| **Packages per second** | Classified items divided by elapsed batch processing time. Freeze the final value at completion. |
| **HTTP latency p50 / p95** | Median and 95th percentile of successful HTTP calls in this run. |

Display available measurements as the run proceeds and keep the final scoreboard visible while the presenter inspects results. The compact, collapsible technical log shows the package ID, timestamp, and milestone or error. The metrics are for the observed workload and deployment.

See [global specification](../global.md#measure-the-live-run) and [implementation tasks](tasks.md).
