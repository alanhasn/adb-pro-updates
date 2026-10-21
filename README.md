# ADB PRO — updates

This tiny public repo exists for one reason: **ADB PRO** (the main app lives
in a separate, private repository) checks `update.json` here on startup to
see if a newer version exists, and shows a one-line "update available"
notice if so.

**This repo only ever holds a version number and a one-line note — never the
EXE itself, and never a public download link.** ADB PRO is a PyInstaller
build, which can be decompiled close to its original Python source (and
that source embeds the license-signing secret) - so the compiled app must
never be publicly downloadable. It's built automatically on every push (see
`.github/workflows/build-and-release.yml` in the main repo) as a **private**
Actions artifact, and handed to each shop directly by the developer.

## Shipping a new version

1. Bump `VERSION` in `core/version.py` in the main app repo and push to
   `main` — CI builds the EXE and bumps `update.json` here automatically.
2. Download the built EXE from that run's private Actions artifact (only
   visible to people with access to the main repo) and send it to the shop
   yourself, the same way as any other update.

## update.json format

```json
{
  "version": "1.2.0",
  "notes": "One-line summary of what changed, shown in the in-app notice."
}
```

No `url` field — the in-app notice is informational only ("a new version is
out, contact the developer"), it never links anywhere public.
