# MDViewer releases

Published builds of **MDViewer**, a standalone Windows Markdown viewer and editor. This
repository holds the installers and the update manifest. The source lives elsewhere and is
not public.

## What is here

| | |
|---|---|
| `latest.json` | The update manifest MDViewer reads when you choose `Help ▸ Check for updates…` |
| Release assets | `MDViewer-Setup.exe`, attached to each `v<version>` tag |

## Installing

Download `MDViewer-Setup.exe` from the [latest release](../../releases/latest) and run it.

MDViewer is self-contained: it needs no .NET runtime, no WebView2 runtime and no internet
connection. It carries its own browser engine, which is why the download is large.

**The installer is not code-signed**, so Windows SmartScreen will warn you before it runs.
If you would rather check the download yourself than trust that dialog, compare its hash
against the `sha256` field in [`latest.json`](latest.json):

```powershell
(Get-FileHash .\MDViewer-Setup.exe -Algorithm SHA256).Hash.ToLowerInvariant()
```

## Updating

MDViewer checks for updates **only when you ask it to**, from `Help ▸ Check for updates…`.
There is no background check, no check at startup, no timer, and no setting that turns one
on. Nothing is downloaded until you confirm a second time, and the dialog shows the new
version, the WebView2 engine it carries and the download size before you do.

The check reads `latest.json` from this repository's `main` branch, then downloads the
installer named there and verifies it against the recorded SHA-256. A file that does not
match is deleted and never run.

## Why the manifest lives on a branch

`latest.json` is committed to `main` rather than attached to a release, so its URL never
moves as versions come and go:

```
https://raw.githubusercontent.com/kyrby/MDViewer-releases/main/latest.json
```

Installed copies have that address compiled in. It is not configurable, deliberately — a
setting that pointed the update check somewhere else would be the most useful thing in the
application to anyone who could edit a settings file.
