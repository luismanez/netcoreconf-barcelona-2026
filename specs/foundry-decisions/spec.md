# Feature — Foundry decisions

Each ready package gets one live call to Microsoft-Decision-1.1 through `POST /providers/microsoft/v1/systemone`. The app sends a shared state containing the operator note and image reference. The image asset contains the package photo as base64. The request uses the configured Foundry deployment name.

| Answer key | Type | Meaning |
| --- | --- | --- |
| `visible_damage` | `noul` | Estimated probability of visible damage to the exterior packaging in the photo |
| `route` | `choice` | Continue, Repack, or Inspect with the distribution across all three options |
| `urgency` | `score` | Numeric score across Low, Normal, High, and Critical, ordered from 0 to 3 |

Provide the parsed result, raw response JSON, and measured HTTP duration to the batch. Surface configuration, HTTP, timeout, and unusable-response failures with an actionable reason. The app uses server-side credentials to call Foundry.

See [global specification](../global.md#decide-what-to-do-with-each-package), [Microsoft Learn](https://learn.microsoft.com/en-us/azure/foundry/foundry-models/how-to/use-foundry-models-microsoft-decision), and [implementation tasks](tasks.md).
