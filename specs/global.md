# Package Sorting Demo

## Purpose

Build a web demo for NetCoreConf Barcelona 2026 with a React and TypeScript interface and an ASP.NET Core Minimal API backend on .NET 10. It shows how Microsoft-Decision-1.1 turns a package photo and a warehouse note into decisions an application can act on. The presenter operates a simulated conveyor belt. The audience can follow a single decision, watch a batch sort live, and inspect the evidence and timing for any package.

The demo uses Microsoft-Decision-1.1 in Microsoft Foundry through the System One endpoint. The talk opens the technical walkthrough with a raw HTTP request to `POST /providers/microsoft/v1/systemone` and applies the same contract in the .NET app. One comparison slide covers Azure OpenAI Decisions API and GPT-6 Luna. [Microsoft-Decision-1.1 in Foundry](https://learn.microsoft.com/en-us/azure/foundry/foundry-models/how-to/use-foundry-models-microsoft-decision) · [Azure OpenAI Decisions API](https://learn.microsoft.com/en-us/azure/foundry/openai/how-to/decisions)

## Load the packages

- The web app has a file drop area. The presenter can drag in one image or a prepared batch of images from the file explorer. The planned stage batch is approximately 48 to 60 packages.
- Each filename carries a package ID. For example, the app looks up `P024.jpg` under `P024` in a preloaded JSON manifest that represents the warehouse records.
- The manifest supplies the operator note automatically. A note can contain the declared contents, handling context, observed issues, and the pickup deadline. For example, "Contains six glass tumblers. Next pickup is in 20 minutes. The operator heard a rattle."
- Every ready package appears in the incoming queue with its ID and photo. A photo the app cannot read or match to a note shows a package-level intake error with its reason. The remaining packages can proceed.

## Decide what to do with each package

Send one live Foundry request per package with its photo and matched note. The note and the image reference go in `state`, and the photo is supplied in `assets`. The three questions share that context and each returns its own answer. [Image input and combined questions](https://learn.microsoft.com/en-us/azure/foundry/foundry-models/how-to/use-foundry-models-microsoft-decision#use-an-image-as-input)

| Type | Question | How the app uses the answer |
| --- | --- | --- |
| `noul` | Does the photo show visible damage to the packaging? | Show the estimated probability from 0 to 1. The question asks the model to assess the photo. |
| `choice` | Given the photo and the note, what should happen to the package? | Show the selected route and the probability for each option. The app uses those probabilities to decide whether to apply the proposed route automatically. |
| `score` | How urgently does the package need attention given the photo and the note? | Show an urgency score with a visual treatment and a text label. The ordered levels are Low, Normal, High, and Critical. The response can contain fractional scores across the 0–3 scale. |

### Routing policy

| Destination | When it applies |
| --- | --- |
| **Continue** | The package can proceed as it is. |
| **Repack** | The exterior packaging needs repair or replacement and the evidence suggests the contents can proceed after repacking. |
| **Inspect** | The evidence suggests the contents need inspection, or the application requests human review because the proposed route falls below the threshold. |

The app compares the probability assigned to the selected route with the review threshold. When the probability meets the threshold, the app applies that route. When it falls below the threshold, the app sends the package to **Inspect** with a **Human review** label. The package details show the model's proposed route, the applied route, and the rule that led to it.

The presenter can change the threshold for a selected result and watch the routing policy run again using the stored answer. For example, a proposed **Repack** route at 72% goes to **Repack** at a 65% threshold and to **Inspect** for human review at an 85% threshold. These figures illustrate the behavior. The original Foundry response and its timing are retained during the policy replay.

## Watch the conveyor run

- The projection view shows incoming packages, packages being processed, and the three destination lanes. The package ID, photo, lane, and urgency label are legible from the back of the room.
- The app processes multiple packages in parallel with a limit on in-flight requests. Eight concurrent calls is a rehearsal starting point. The setting used on stage depends on measured latency and the deployment's allocated quota. [Microsoft Foundry quotas](https://learn.microsoft.com/en-gb/azure/foundry/foundry-models/quotas-limits?view=foundry#microsoft-decision-11-quotas)
- As each valid response arrives, the app updates the scoreboard and animates the package into its applied lane. Packages can finish in any order. The package ID keeps each photo, note, decision, and timing together.
- A failed Foundry call appears as a failed package with an inspectable reason. The app continues processing the rest of the batch.
- A collapsible technical log shows package IDs, timestamps, and processing milestones live, including queue entry, request start, response arrival, route application, and any failure.

### Package details

Clicking a sorted package opens a panel with its ID, original photo, and operator note. The panel shows the visible-damage probability, all route probabilities, the proposed and applied routes, the urgency score and label, and any human-review reason. It also shows the raw Foundry response JSON, the queue wait, and the HTTP call duration. For a failed package, the panel shows its error and any timing available.

## Measure the live run

The backend starts the batch clock once the photos are loaded and live processing begins. It stops when every package has reached a final result or a recorded failure. The animation uses the results as they arrive, so the scoreboard reflects processing progress as measured on the backend.

| Scoreboard value | Definition |
| --- | --- |
| **Packages classified / total** | Packages with a valid Foundry response and an applied destination, including packages sent for human review, divided by the total number of photos submitted in the batch. Intake and processing errors are visible as separate counts. |
| **Packages per second** | Successfully classified packages divided by elapsed batch processing time. The value updates during the run and shows the final rate when the batch finishes. |
| **HTTP latency p50 / p95** | The median and 95th percentile of completed, successful Foundry calls in the current run. Each timing starts when the backend sends the request and ends when it receives the complete response body. |

The individual call duration includes the network round trip and the service response time observed by the backend. The batch rate shows how quickly the line moves with concurrent requests. The stage demo reports measurements from the live run with its own photos, notes, and Foundry deployment.

## Stage walkthrough

1. **Start with one package.** Show a photo and the associated note, invite the audience to pick a route, and walk through the raw HTTP request and its three typed answers. Then classify a package in the web app so the audience can follow the result and see the real call duration.
2. **Drop the batch.** Load the prepared photo set and start the live run. As the belt sorts the packages, follow the scoreboard and point out the urgency labels on the destination lanes.
3. **Inspect the evidence.** Open a finished package to show its photo, note, raw answer, and timings. Use two prepared cases with the same photo and different contents, such as glassware and T-shirts, to show how the note can change the recommended route or urgency. Select examples whose behavior has been checked during rehearsal.
4. **Change the threshold.** Open a borderline result and adjust the routing threshold. Show the same package moving from its proposed lane to human review under the stricter policy.

The prepared dataset should cover straightforward examples for each destination, multiple urgency levels, a pair that demonstrates the effect of the text, and a suitable case for the threshold replay.

## Acceptance criteria

- Dragging in one prepared photo or a full stage batch matches each photo to its note by package ID and shows it on the belt.
- A valid package produces one Foundry request with the matching photo, note, and all three question types. Its result is associated with the correct package even when responses arrive out of order.
- During the batch, packages move into their applied lanes, urgency is readable in color and text, and the technical log follows the run.
- A completed package can be inspected from its destination lane. Its detail panel shows the actual Foundry response, decoded decisions, and measured timings.
- Changing the review threshold for a borderline result updates its applied route using the stored answer and preserves the live run's request count and timing data.
- The scoreboard reports the measured run's successful classifications, throughput, and HTTP latency percentiles. Intake errors and failed Foundry calls remain visible, and the rest of the batch can complete.
