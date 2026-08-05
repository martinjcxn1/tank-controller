# Releasing firmware

Devices update themselves over the air. You cut a release on GitHub; each unit's
owner presses **Install Firmware Update** in the web UI and their device pulls
the new binary and self-flashes. No build machine, no per-device work.

## Cut a release

Two ways to trigger a build (both run on GitHub's servers — your PC can be off):

**Tag push (recommended):**

```bash
git tag v2026.8.5
git push origin v2026.8.5
```

**Manual:** GitHub repo → **Actions** tab → *Build & Release Firmware* →
**Run workflow** → enter a version like `v2026.8.5`.

Either way, GitHub Actions:

1. Compiles `tankcontroller.yaml` (ESPHome pinned in the workflow).
2. Computes the OTA binary's md5 and writes `manifest.json`.
3. Publishes a **Release** with `tankcontroller.ota.bin`, `tankcontroller.factory.bin`, and `manifest.json` attached.

Watch progress in the **Actions** tab. Green tick = release is live.

## How devices consume it

Firmware has a `update: http_request` entity pointed at
`releases/latest/download/manifest.json`. It polls every 6h and compares its
running version against the manifest `version`. When the owner presses **Install
Firmware Update**, the device re-checks, and installs only if a newer version is
advertised (a press on the latest firmware is a safe no-op). On success the
device reboots into the new image.

## Versioning

The manifest `version` comes from the tag with the leading `v` stripped
(`v2026.8.5` → `2026.8.5`). **Always bump the tag** — the update entity only
flags an update when the manifest version differs from what's running. Reusing a
tag means devices won't see a new version.

## First flash (new unit)

OTA only works once a device is already running this firmware. Flash a brand-new
board over USB with `tankcontroller.factory.bin` (via ESPHome Web / esptool);
after that it self-updates.

## Notes

- **No secrets in the repo.** WiFi is provisioned per-unit via the captive
  portal, so the public binary carries no credentials. Keep it that way — don't
  hardcode network creds in the YAML.
- **ESPHome version** is pinned in `.github/workflows/build-firmware.yml`
  (`version:`). Bump it when you upgrade your local ESPHome so CI matches.
- **Don't interrupt active cycles.** An OTA reboot mid-dose or mid-water-change
  will break the cycle. Consider guarding the install button against active
  states if that becomes a problem in the field.
