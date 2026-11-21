# Tasks — Package intake

Paths are relative to `src/PackageSortingDemo`. Track completion in the [checklist](../tasks/todo.md).

## ING-01

**Scaffold the local demo app**

Scaffold the .NET 10 Minimal API host and the single-screen Vite React and TypeScript app in `ClientApp`. Keep the npm lockfile. Build the frontend into the generated `wwwroot/app/` directory and serve it from the ASP.NET Core origin alongside the API.

- **Acceptance.** Both builds succeed and the ASP.NET Core URL opens the React screen.
- **Dependencies.** None.
- **Likely files.** `PackageSortingDemo.csproj`, `Program.cs`, `ClientApp/package.json`, `ClientApp/vite.config.ts`, `ClientApp/src/App.tsx`.

## ING-02

**Stage photos and attach warehouse notes**

Add the multipart staging endpoint and use ASP.NET Core's built-in antiforgery token. Read the note from the JSON manifest using the filename stem. Use generated item IDs for the uploads and enforce image format and size limits appropriate to the stage set.

- **Acceptance.** Each readable PNG or JPEG with a matching note is ready. An unreadable photo or missing note has a package-level reason. Ready items in the same batch can proceed.
- **Dependencies.** ING-01.
- **Likely files.** `Program.cs`, `Intake/BatchIntake.cs`, `Intake/ManifestReader.cs`, `Batches/BatchStore.cs`, `Data/packages.json`.

## ING-03

**Load a batch from the React screen**

Add the file drop area and picker. Submit the photos through the same-origin API and use the returned item IDs to match the previews to the staged entries.

- **Acceptance.** Dropping one photo or the stage set populates the queue with photos, matching notes, and any intake errors.
- **Dependencies.** ING-02.
- **Likely files.** `ClientApp/src/App.tsx`, `ClientApp/src/components/PackageIntake.tsx`, `ClientApp/src/api.ts`, `ClientApp/src/contracts.ts`.
