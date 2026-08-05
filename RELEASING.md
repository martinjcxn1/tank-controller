# Releasing firmware

Releases are **fully automated**. You don't touch a version number. Merge
firmware changes to `main` and GitHub builds, versions, and publishes the
release. Each unit's owner then presses **Install Firmware Update** in the web UI
and their device pulls the new binary and self-flashes.

## Ship a release

1. Make firmware changes in a branch/PR (editing `tankcontroller.yaml`).
2. Merge to `main`.

That's it. On the merge, `.github/workflows/build-firmware.yml`:

1. Generates a version from the current UTC time (e.g. `2026.08.05.1430`).
2. Injects it into the firmware, replacing the `0.0.0-dev` sentinel, then compiles — so the binary reports that exact version.
3. Computes the compiled binary's md5 and compares it to the latest release. If the binary is byte-identical (e.g. a comment-only change), it stops — nothing to ship.
4. Otherwise generates `manifest.json`, tags `v<version>` on the merge commit, and publishes a **Release** with `tankcontroller.ota.bin`, `tankcontroller.factory.bin`, and `manifest.json`.

Watch it in the **Actions** tab. You can also trigger a run manually there
(*Run workflow*).

## Why timestamps, and why you never edit the version

The device compares its own running version against the manifest version. If you
hand-set a version and forgot to bump it, updates wouldn't be detected; if CI
invented one but didn't bake it into the binary, devices would think an update
was *always* available. The timestamp scheme sidesteps both: every build gets a
unique, monotonically increasing version that is stamped into the binary and the
manifest together. The `version:` line in `tankcontroller.yaml` stays at
`0.0.0-dev` — that's only what a local dev build reports; CI overwrites it.

**Do not hand-edit the `project.version` line for releases.** It's CI-managed.

## What triggers a release

Only pushes to `main` that touch `tankcontroller.yaml` (or the workflow itself)
run the build — docs/other changes are ignored. And even then, a release is
published only if the compiled binary actually differs from the last one. So no
merge ever ships a redundant "update."

## First flash (new unit)

OTA only works once a device is already running this firmware. Flash a brand-new
board over USB with `tankcontroller.factory.bin` (via ESPHome Web / esptool);
after that it self-updates. A fresh local/USB build reports version `0.0.0-dev`,
so it will immediately see the latest release as an available update — expected.

## How devices consume it

Firmware has a `update: http_request` entity pointed at
`releases/latest/download/manifest.json`. It polls every 6h and compares its
running version against the manifest. The owner's **Install Firmware Update**
button re-checks and installs only if a newer version is advertised; the install
is blocked while a dose or water change is running. On success the device reboots
into the new image.

## Notes

- **No secrets in the repo.** WiFi is provisioned per-unit via the captive
  portal, so the public binary carries no credentials. Keep it that way.
- **ESPHome version** is pinned in the workflow (`version:`). Bump it when you
  upgrade your local ESPHome so CI matches.
