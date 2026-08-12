# Tank Controller

ESPHome firmware for a custom ESP32-based aquarium and reef tank controller.

It automates water changes, auto top-off (ATO), reservoir refilling, dosing, heating
and cooling, CO2 and scheduled mains equipment — and runs **standalone**. All control
logic lives on the device; Home Assistant is optional, and the unit keeps dosing and
topping up with no network at all.

---

## What it controls

| | |
|---|---|
| **4 × mains (AC) outlets** | Heater, lights, return pump, skimmer. Per-outlet mode: Off / Always On / Scheduled / Heater |
| **8 × low-voltage (DC) outputs** | Drain and fill pumps, up to six dosing pumps, cooling fan, CO2 valve, ATO pump, ATO fill solenoid |
| **Sensors** | Tank temperature (DS18B20), optical level, leak detector, 2 × assignable float switches, CO2 bottle load cell |

Outputs DC 4–8 are dual-role: each is either a doser or its dedicated function,
selected at runtime from the web UI.

### Automations

- **Water change** — scheduled per weekday, timed drain with a ratio-based fill,
  optional simultaneous (overlapping) mode. Stop / Continue / Cancel, plus Drain Only
  and Fill Only. Survives a reboot in a paused state.
- **ATO** — continuous top-off on the optical level sensor, with a runtime cap that
  stops the ATO until an operator clears it. Salt-water mode routes top-up through a
  dedicated pump so salinity stays stable.
- **ATO Fill** — scheduled solenoid top-up, gated on a float assigned to *ATO Full*.
- **Reservoir Fill** — scheduled refill of the new-water reservoir via a solenoid.
- **Dosing** — six pumps, volume-based (mL) with per-pump mL/s calibration, one dose
  per day, plus manual dose / stop / flush.
- **Temperature** — ESPHome thermostat in heat/cool mode driving any AC outlet set to
  Heater and the fan on DC 5.

Every automation shares the same interlocks: a leak, an empty reservoir, a full waste
container or a high-level failsafe pauses it, and it resumes with **Continue**.

---

## Repository layout

```
tankcontroller.yaml       The firmware. Single source of truth
instruction-manual.md     End-user manual (Markdown)
Tank_Controller_User_Manual.docx   Same manual, formatted for print/PDF
RELEASING.md              How releases are built and shipped
.github/workflows/        CI: build, version, publish
```

---

## Building and flashing

Requires [ESPHome](https://esphome.io) **2026.7.3** (the version CI pins — keep local
builds matching).

```bash
esphome config  tankcontroller.yaml     # validate
esphome compile tankcontroller.yaml     # build
esphome run     tankcontroller.yaml     # build + flash + logs
```

No `secrets.yaml` is needed. WiFi is **not** compiled in — a fresh device boots into
its own access point (`Tank Controller` / `tankcontroller`) and is provisioned through
the captive portal at `192.168.4.1`. That also means the published binaries carry no
credentials; keep it that way.

**New boards** must be flashed once over USB with `tankcontroller.factory.bin`. After
that they self-update over the air.

---

## Releases and OTA

Releases are fully automated — you never set a version number. Merge a change to
`tankcontroller.yaml` on `main` and CI generates a UTC-timestamp version, injects it,
builds, and publishes only if the compiled binary actually changed.

Devices poll a manifest on **GitHub Pages** every 6 hours and expose a *Firmware
Update* entity. Installing is owner-triggered from the web UI, never automatic, and is
refused while a dose or water change is in progress.

See **[RELEASING.md](RELEASING.md)** for the full pipeline and the one-time Pages setup.

---

## Hardware

- **MCU** — ESP32-WROOM DevKit (38-pin), `esp32dev`, ESP-IDF framework
- **I²C** (GPIO22/21, 100 kHz) — MCP23008 @ 0x20 driving the 8 DC outputs; DS3231 RTC
  @ 0x68 for battery-backed time
- **1-Wire** — DS18B20 on GPIO4 (needs a 4.7 kΩ pull-up)
- **HX711** — CO2 bottle load cell on GPIO33/32
- **Inputs** — leak GPIO25, float 1 GPIO36, float 2 GPIO39, optical level GPIO34
- **AC relays** — GPIO16–19, active high

### Level input convention

Every level input reads **OFF when its condition is met**, and ON when it is not. The
switches are pulled up and close on the condition, so a disconnected or failed input
sits ON — read as *"condition not met"* — rather than silently reporting a level it
cannot see. The optical sensor's module output is the opposite way round, so it is
inverted at the pin to match. Nothing is inverted for display: what the UI shows is the
value the control logic uses.

---

## Documentation

- **[instruction-manual.md](instruction-manual.md)** — full end-user manual: setup,
  every section of the UI, troubleshooting by symptom, and a settings quick reference.
- **[RELEASING.md](RELEASING.md)** — release process and OTA design notes.

---

## License

GNU General Public License v3.0 — see [LICENSE](LICENSE).
