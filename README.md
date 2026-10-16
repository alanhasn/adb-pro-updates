# ADB PRO — updates

This tiny public repo exists for one reason: **ADB PRO** (the main app lives
in a separate, private repository) checks `update.json` here on startup to
see if a newer version exists, and shows a one-line "update available" notice
if so. No source code or customer data lives here — just a version manifest
and, as GitHub Releases, the downloadable `.exe` for each version.

## Shipping a new version

1. Bump `VERSION` in `core/version.py` in the main app repo.
2. Build the new EXE (see the main repo's Readme).
3. In this repo: `gh release create vX.Y.Z path\to\ADB_PRO.exe --title "vX.Y.Z" --notes "What changed"`
4. Update `update.json` here: bump `"version"` to match, update `"notes"` to
   a short one-line summary, then commit + push.

The app re-checks `update.json` every time it starts (silently skips the
check if there's no internet — it never blocks startup).

## update.json format

```json
{
  "version": "1.2.0",
  "url": "https://github.com/alanhasn/adb-pro-updates/releases/latest",
  "notes": "One-line summary of what changed, shown in the in-app notice."
}
```
