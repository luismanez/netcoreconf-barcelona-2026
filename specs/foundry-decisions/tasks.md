# Tasks — Foundry decisions

Paths are relative to `src/PackageSortingDemo`. Track completion in the [checklist](../tasks/todo.md).

## DEC-01

**Call Microsoft-Decision-1.1 for a package**

Use a typed `HttpClient` with server-side Foundry settings. Build one System One request with the operator note in `state`, the referenced photo in `assets`, and the named `noul`, `choice`, and `score` questions. Parse the typed answers, retain the raw response, and measure elapsed HTTP time through complete body receipt. Make provider and response errors available to the package detail panel. [Microsoft Learn](https://learn.microsoft.com/en-us/azure/foundry/foundry-models/how-to/use-foundry-models-microsoft-decision)

- **Acceptance.** A successful live call yields the damage probability, route and its option probabilities, urgency score, raw JSON, and call duration. A missing configuration, timeout, rate limit, or unusable answer produces a readable reason for the affected package.
- **Dependencies.** ING-02.
- **Likely files.** `Program.cs`, `appsettings.json`, `Foundry/FoundryOptions.cs`, `Foundry/FoundryClient.cs`, `Foundry/DecisionResult.cs`.
