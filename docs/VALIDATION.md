# Validation

Authoring date: November 6, 2026. Host: Windows. Target: Windows desktop.

## Local result

Target-platform source CI is recorded after publication. This host has Python, Node.js, and .NET; other native toolchains are verified through CI. No unobserved GUI/device behavior is claimed.

## Reproducible checks

The GitHub Actions workflow builds/runs the following on `windows-latest`:

```sh
dotnet build
dotnet run --no-build -- --self-test
```

## Manual acceptance

Start capture, copy two synthetic strings, select/copy an earlier entry, stop capture, and clear memory. Export only a synthetic selected string. Also test malformed inputs and an unwritable output destination.

A workflow file is not evidence of a passing run. Observed CI run links and source commits are recorded after publication. Native GUI, sound, sleep/resume, and platform permissions require direct target-platform acceptance even when model tests pass.
