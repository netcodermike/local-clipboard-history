# Local Clipboard History

Keep an explicitly enabled, memory-only Windows clipboard text history.

[![Build and verify](https://github.com/netcodermike/local-clipboard-history/actions/workflows/verify.yml/badge.svg)](https://github.com/netcodermike/local-clipboard-history/actions/workflows/verify.yml)

**Language:** C# · **Platform:** Windows desktop · **App type:** Windows local clipboard organizer

First-release learning implementation, with explicit scope below. This is one independently runnable app, not a placeholder in a combined repository.

## Features

- Capture starts OFF
- One-second text polling
- Deduplicated 50-item history
- Copy/clear/export selected text

## Requirements

.NET 10 SDK/Windows Desktop runtime. WPF runs only on Windows. No NuGet packages.

## Quick start

```sh
git clone https://github.com/netcodermike/local-clipboard-history.git
cd local-clipboard-history
dotnet run
```

Commands run from the repository root. Lines marked for a particular operating system apply only there. Language tools are prerequisites, not installed by the app. Close desktop windows normally; terminal/server apps stop with Ctrl+C unless their usage notes say otherwise.

## Example workflow

Start capture, copy two synthetic strings, select/copy an earlier entry, stop capture, and clear memory. Export only a synthetic selected string.

## Architecture, configuration, and data

Program.cs separates a History model from WPF controls. Start/stop toggles polling; a changed clipboard string is moved to the front if nonempty and at most 20,000 characters. No content is captured during self-tests. The model test verifies deduplication/order/cap. History is lost on exit unless the user explicitly exports a selected entry. Clipboard busy errors retry on the next tick.

## Verification

Build with the quick-start command where needed, then run:

```sh
dotnet run -- --self-test
```

Manual acceptance: Start capture, copy two synthetic strings, select/copy an earlier entry, stop capture, and clear memory. Export only a synthetic selected string. Also test malformed inputs and an unwritable output destination.

See [validation record](docs/VALIDATION.md) for observed checks and their limits. CI results verify only what the workflow runs; they do not establish native GUI correctness or production readiness.

## Limitations and next steps

Text only; no rich formats, pinning, persistence, autostart, encryption, password detection, or private-mode awareness. Any copied sensitive text can be included after capture is enabled. Clearing does not clear the system clipboard. Polling can miss rapid changes. Output export replaces the chosen file.

## Troubleshooting

Use the exact platform/toolchain above. Preserve originals and use synthetic fixtures first. Errors are displayed in the UI or stderr. A headless machine can run the model tests but cannot verify native GUI/audio behavior. Output paths are chosen explicitly; keep backups of important data.

## Source map

- `App.csproj`
- `Program.cs`

## Development and license

Read [contributing](CONTRIBUTING.md) before changing the app, and [security/privacy](SECURITY.md) before supplying private data. Use synthetic fixtures for tests. No telemetry, paid API key, or account is required by the app itself. Dependencies, when present, are stated in Requirements.

[MIT license](LICENSE), copyright 2026 netcodermike.
