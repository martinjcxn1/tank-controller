# Tank Controller — User Manual

**Aquarium & Reef Automation System**
Setup, Configuration and Daily Use

---

## Contents

1. [About Your Controller](#1-about-your-controller)
2. [What Plugs In Where](#2-what-plugs-in-where)
3. [First-Time Setup](#3-first-time-setup)
4. [Finding Your Way Around](#4-finding-your-way-around)
5. [Temperature Control](#5-temperature-control)
6. [Automatic Top-Up (ATO)](#6-automatic-top-up-ato)
7. [Water Changes](#7-water-changes)
8. [Reservoir Fill](#8-reservoir-fill)
9. [Float Switches](#9-float-switches)
10. [Dosing](#10-dosing)
11. [Mains Outlets](#11-mains-outlets)
12. [Settings](#12-settings)
13. [Troubleshooting](#13-troubleshooting)
14. [Quick Reference](#14-quick-reference)

*New to the controller? Read sections 3 and 4 first, then set up only the features you need.*

---

## 1. About Your Controller

The Tank Controller automates the routine jobs of running an aquarium or reef tank: water changes, topping up evaporated water, dosing additives, controlling heating and cooling, and switching mains equipment on a schedule.

Everything is controlled from a web page in your browser — on a phone, tablet or computer. There is no app to install and no account to create. Once configured, the controller runs entirely on its own; it does not need the internet or your phone to keep working.

### What it controls

- **4 mains (AC) outlets** — for heaters, lights, pumps, skimmers and similar equipment.
- **8 low-voltage (DC) outputs** — for dosing pumps, water-change pumps, cooling fans, CO2 and solenoid valves.
- **Sensors** — tank temperature, water level, leak detection, two float switches, and CO2 bottle weight.

Each feature has its own section in the control panel, so you only need to set up the parts you actually use.

> **Safety** — Mains voltage is present inside this unit. Always switch off and unplug before opening the enclosure or changing any connection. If a leak is detected, disconnect power at the wall before investigating.

---

## 2. What Plugs In Where

Your installer or supplier will normally have connected everything for you. This section is a short overview so the settings later in the manual make sense.

### Mains outlets (AC 1 – AC 4)

Four switched mains outlets. Typical use: a heater, the display lights, a return pump and a skimmer. Each outlet can be named and given its own schedule.

### Low-voltage outputs (DC 1 – DC 8)

| Output | Normally used for | Can be changed? |
|---|---|---|
| DC 1 | Drainage pump (removes old tank water) | Fixed |
| DC 2 | Filling pump (adds new water) | Fixed |
| DC 3 | Dosing pump | Fixed |
| DC 4 | Dosing pump, or reservoir refill solenoid | Yes |
| DC 5 | Cooling fan, or dosing pump | Yes |
| DC 6 | CO2 valve, or dosing pump | Yes |
| DC 7 | Auto top-up (ATO) pump, or dosing pump | Yes |
| DC 8 | ATO Fill solenoid valve, or dosing pump | Yes |

Outputs marked "Yes" have a Role setting in the **Settings** section. Changing the role changes what that output does — see section 12.

### Sensors

- **Tank temperature** — a waterproof probe in the tank or sump. Used for heating and cooling.
- **Water level (optical sensor)** — mounted at your normal water line. Tells the controller when evaporation has dropped the level and a top-up is needed.
- **Leak detector** — placed on the floor or in the cabinet. If it gets wet, the controller stops all water movement.
- **Float 1 and Float 2** — two switches you assign to jobs such as "reservoir empty" or "drainage container full". See section 9.
- **CO2 bottle scale** — optional load cell under the CO2 cylinder to show how much gas is left.

---

## 3. First-Time Setup

This takes about five minutes. You will need the WiFi name and password for your home network.

### Step 1 — Power on

1. Plug the controller in and switch it on.
2. Wait about 30 seconds for it to start up.

### Step 2 — Connect to the controller

The first time it starts, the controller creates its own temporary WiFi network so you can reach it.

1. On your phone or laptop, open your WiFi settings.
2. Connect to the network named **Tank Controller**.
3. Enter the password: `tankcontroller`

> **Tip** — Your phone may warn that this network has no internet access. That is normal — stay connected to it for the next step.

### Step 3 — Join your home WiFi

1. A setup page should open automatically. If it does not, open a browser and go to `192.168.4.1`
2. Choose your home WiFi network from the list.
3. Enter your WiFi password and save.
4. The controller restarts and joins your network. Its own temporary network disappears.

You only ever do this once. The controller remembers your WiFi and reconnects automatically after a power cut.

### Step 4 — Open the control panel

1. Reconnect your phone or laptop to your normal home WiFi.
2. In a browser, go to: `tankcontroller.local`
3. The control panel opens. Bookmark this page.

> **If that address does not work** — Some networks do not support `.local` names. Find the controller's IP address in your router's device list (it appears as "tankcontroller") and use that address instead, for example `192.168.1.42`

### Step 5 — Check the clock

At the top of the Status & Sensors section you will see **Date / Time**. It should show the correct local date and time within a minute of connecting. All schedules depend on this being right.

---

## 4. Finding Your Way Around

The control panel is divided into sections. Each one groups related settings together.

| Section | What it covers |
|---|---|
| Status & Sensors | Live readings: time, temperature, leak, floats, water level |
| Temperature Control | The thermostat — heating and cooling |
| Water Change Settings | How a water change runs, plus manual start/stop buttons |
| Water Change Schedule | Which days and what time water changes happen |
| ATO | Automatic top-up of evaporated water |
| ATO Fill | Scheduled top-up through a solenoid valve |
| Reservoir Fill | Automatic refilling of your new-water reservoir |
| DC Outputs | Manual control of the low-voltage outputs |
| AC Outputs | Mains outlet schedules and manual control |
| CO2 & Cooling | CO2 on/off times |
| Calibration | CO2 bottle weight and scale setup |
| Doser 3 – Doser 8 | One section per dosing pump — everything for that pump |
| Settings | Names and roles for every output and float |

### Buttons you will see everywhere

Most automatic processes share the same set of four buttons. They behave consistently:

| Button | What it does |
|---|---|
| Start Now | Begins the process immediately, without waiting for its schedule |
| Stop | Pauses the process and switches its pumps off. Progress is remembered |
| Continue | Resumes a paused process from exactly where it stopped |
| Cancel | Clears the process completely so it can be started again from the beginning |

> **Stop vs Cancel** — Use Stop if you want to resume later, for example to top up a reservoir mid-way through a water change. Use Cancel if you want to abandon the run entirely and start fresh.

---

## 5. Temperature Control

Heating and cooling are handled by a single thermostat, found in the Temperature Control section.

### Setting your temperatures

The thermostat card has two temperature targets:

- **Lower target** — heating switches on if the tank falls below this. Default 25 °C.
- **Upper target** — cooling switches on if the tank rises above this. Default 28 °C.

Adjust them on the thermostat card. They move in 0.5 °C steps, and there is a built-in 0.3 °C tolerance so equipment does not switch rapidly on and off around the setpoint.

### Thermostat modes

| Mode | Behaviour |
|---|---|
| Heat/Cool | Both heating and cooling active. Recommended for most tanks |
| Heat | Heating only |
| Cool | Cooling only |
| Off | No heating or cooling at all |

### Connecting your heater

Heating works through the mains outlets. Go to the **Settings** section, find the outlet your heater is plugged into, and set its Mode to **Heater**. You can set more than one outlet to Heater if you run two heaters.

### Connecting your cooling fan

Cooling works through output DC 5. In the **Settings** section at the bottom of the page, set **DC 5 Role** to **Cooling Fan**. If you do not have a fan, leave the role as it is — nothing will happen when the tank gets warm.

> **Safety** — If the temperature probe fails or is unplugged, all heating and cooling switch off automatically rather than running unchecked.

---

## 6. Automatic Top-Up (ATO)

As water evaporates, the level in your tank drops. The ATO tops it back up automatically using fresh water from a reservoir. Settings are in the ATO section.

### Salt water or fresh water?

This is the first thing to set, because it changes which pump the ATO uses.

| Setting | Use when | What the ATO uses |
|---|---|---|
| Salt Water — ON | Marine / reef tank | The dedicated ATO pump on DC 7 |
| Salt Water — OFF | Freshwater tank | The filling pump on DC 2 |

On a marine tank only fresh water is added, because salt does not evaporate. That is why a separate top-up pump is used.

### Everyday settings

- **ATO Enabled** — the master switch. Turn off to stop all automatic topping up (for example while doing tank maintenance).
- **ATO Max Runtime** — a safety limit in seconds. The pump will never run longer than this in one go. Default 120 seconds.

### Buttons

- **Top Up Now** — runs a top-up immediately, even if ATO Enabled is off. Does nothing if the tank is already full.
- **Stop** — pauses topping up.
- **Continue** — resumes it.
- **Cancel** — clears everything and leaves the ATO stopped. Use this if the ATO seems stuck. Press Continue afterwards to switch it back on.

### ATO Status

This line tells you exactly what the ATO is doing and, if it is not running, why. It is the first place to look if top-ups are not happening.

| Message | Meaning |
|---|---|
| topping up | The pump is running now |
| idle: tank full | Normal. Nothing to do |
| idle: ATO disabled | ATO Enabled is switched off |
| stopped by user | You pressed Stop or Cancel. Press Continue |
| blocked: leak detected | A leak was found. Fix it before continuing |
| blocked: water change active | Normal during a water change. It will resume after |
| blocked: ATO source empty | Your top-up reservoir needs refilling |
| blocked: water level failsafe | The backup high-level float says the tank is full |
| stopped: max runtime reached | The safety limit was hit. Press Top Up Now or Cancel to reset |

### ATO Fill (solenoid top-up)

If your top-up water is gravity-fed through a valve rather than pumped, output DC 8 can open that valve on a daily schedule. This has its own **ATO Fill** section directly below ATO.

Switch **Scheduled ATO Fill** on, choose an **ATO Fill Time**, and set an **ATO Fill Max Runtime**. Filling stops when Float 1 reports the level is reached, or when the maximum runtime expires.

Before it will run, **DC 8 Role** must be set to **ATO Fill** and **Float 1 Role** to **ATO Full**, both in the Settings section. Start Now, Stop, Continue and Cancel work as described in section 4.

---

## 7. Water Changes

The controller can drain a set amount of old water and replace it with new water, either on a schedule or on demand.

There are two sections. **Water Change Settings** holds how a change runs and the manual buttons; **Water Change Schedule** holds when it happens automatically.

### Setting it up

In **Water Change Settings**:

1. Set **Water Change Drain Time** — how many seconds the drainage pump runs. This decides how much water is changed. Time a short test run with a measuring jug to work out the right figure.
2. Set **Water Change Fill Ratio** — see below.

Then in **Water Change Schedule**:

3. Choose a **Water Change Time**.
4. Switch on the days of the week you want (Monday to Sunday).
5. Turn **Scheduled Water Change** on.

### Understanding the fill ratio

Filling is often slower than draining, because new water is usually gravity-fed while draining is pumped. The fill ratio tells the controller how much slower or faster.

| Ratio | Meaning | Example |
|---|---|---|
| 1.0 | Filling and draining take the same time | Both pumped equally |
| 1.5 | Filling takes 50% longer than draining | Typical gravity feed |
| 2.0 | Filling takes twice as long as draining | Slow gravity feed |
| 0.8 | Filling is faster than draining | Strong fill pump |

To find your ratio: time how long the tank takes to drain a set amount, then time how long the same amount takes to refill. Divide the fill time by the drain time.

**Water Change Max Fill Time** is calculated for you and shown as a read-only figure. It is a safety limit — filling always stops by then.

### Normal or simultaneous?

- **Simultaneous WC off (normal)** — the tank drains completely, then refills. Simple and safe. Takes the longest.
- **Simultaneous WC on** — filling begins while draining is still finishing, so the whole change takes less time and the water level stays more stable.

### Manual controls

These buttons are at the bottom of Water Change Settings.

| Button | What it does |
|---|---|
| Start Now | Runs a complete water change immediately |
| Drain Only | Runs just the draining stage |
| Fill Only | Runs just the filling stage |
| Stop | Pauses. Both pumps stop, progress is kept |
| Continue | Resumes from where it stopped |
| Cancel | Abandons the run and clears it |

Drain Only and Fill Only are useful for topping off after maintenance, or for emptying the tank into a bucket. The Stop, Continue and Cancel buttons work with them exactly as they do with a full change.

### Water Change Status

Shows the current stage and progress, for example `draining: 45 / 300 s`, `waiting to fill: 12 s left`, or `filling: 88 / 495 s`. If a change has paused it explains why — for example `paused: leak detected` or `paused: reservoir empty (float 1)`.

### Turning equipment off during a change

Return pumps and skimmers usually should not run while the water level is low. In the AC Outputs and DC Outputs sections, switch on **Off During WC** for any equipment that must pause. It switches off for the whole water change and comes back on automatically afterwards.

This is available for all four mains outlets, and for DC 6 and DC 8.

> **Automatic safety stops** — A water change pauses by itself if a leak is detected, if the new-water reservoir runs empty, or if the waste container becomes full. Fix the cause, then press Continue.

---

## 8. Reservoir Fill

If your new-water reservoir is plumbed to a supply, the controller can refill it automatically. Settings are in the Reservoir Fill section, below ATO and ATO Fill.

Before this can run, three things must be true:

1. **Float 2 Role** is set to **Reservoir Full** (in Settings).
2. **DC 4 Role** is set to **Refill Solenoid** (in Settings).
3. No leak is detected.

Then set a **Reservoir Fill Time**, a **Reservoir Fill Max Runtime**, and switch **Scheduled Reservoir Fill** on. Filling stops as soon as the float says the reservoir is full, or when the maximum runtime is reached — whichever comes first.

Start Now, Stop, Continue and Cancel work as described in section 4.

---

## 9. Float Switches

The two float switches are general-purpose. You tell the controller what each one is watching using **Float 1 Role** and **Float 2 Role**, found in the Settings section at the bottom of the page.

Whatever you choose is displayed above that float in Status & Sensors, so you can always see what each float is watching without leaving the page.

### Float 1 options

| Role | What it does |
|---|---|
| Reservoir Empty | Stops a water change when the new-water reservoir runs dry |
| ATO Empty | Stops topping up when the ATO reservoir runs dry |
| ATO Full | Stops the ATO Fill solenoid when the top-up level is reached |

### Float 2 options

| Role | What it does |
|---|---|
| Reservoir Full | Stops the reservoir refill when full. Required for automatic reservoir filling |
| Drainage Full | Stops a water change when the waste container is full |
| Water Level Failsafe | Backup high-level protection. Stops all topping up and filling |

> **Important** — Only choose a role for a float that is actually connected. If you set a role for a float that is not wired in, the controller may think the reservoir is empty or the tank is full and refuse to run.

---

## 10. Dosing

Up to six outputs can act as dosing pumps. Each has its own section — **Doser 3** through **Doser 8** — containing everything for that pump: its schedule, volume, buttons, calibration rate and flush time.

At the top of each section is the pump's name, taken from its label in Settings. If that output is currently set to do something else, the name reads **"Not in Use"** and the dosing buttons in that section will not run.

### Calibrating a dosing pump

Calibration tells the controller how fast your pump delivers liquid, so it can convert a volume in millilitres into a run time. Do this once per pump. Every setting you need is in that pump's own section.

1. Put the pump outlet into a measuring cylinder.
2. In that pump's own section, set its **Flush/Cal Seconds** to 30.
3. Press that pump's **Flush/Run** button. It runs for exactly 30 seconds.
4. Measure how many millilitres came out.
5. Divide that figure by 30. For example 48 mL ÷ 30 = 1.6.
6. Enter the result in that pump's **Rate (mL/s)** box, just above.

### Setting a daily dose

1. Set the pump's **Volume** in millilitres.
2. Set its **Time** — when it should dose each day.

The controller works out the run time itself. Each pump doses once per day, and the daily record resets at midnight.

### Other dosing buttons

- **Dose Now** — delivers the set volume immediately.
- **Stop Now** — stops that pump straight away.
- **Flush/Run** — runs the pump for a fixed number of seconds. Use for priming new tubing or calibrating.

> **Note** — Outputs DC 4 to DC 8 can each be a doser or something else. Their dosing buttons only work when that output's Role is set to Doser — otherwise the section heading reads "Not in Use". Roles are set in the Settings section.

---

## 11. Mains Outlets

Each of the four mains outlets has a **Mode**, set in the Settings section at the bottom of the page.

| Mode | Behaviour |
|---|---|
| Off | Outlet stays off |
| Always On | Outlet stays on |
| Scheduled | Outlet switches on and off at the times you set |
| Heater | Outlet is controlled by the thermostat |

For Scheduled mode, set the **Schedule On** and **Schedule Off** times for that outlet in the AC Outputs section. Schedules that run overnight are handled correctly — for example on at 20:00 and off at 06:00.

You can rename each outlet using its **Label** box in Settings, so "AC 1" becomes "Display Lights".

### CO2 control

If you run CO2, set **DC 6 Role** to **CO2** in Settings, then set the **CO2 Schedule On** and **CO2 Schedule Off** times in the CO2 & Cooling section. CO2 is usually timed to come on shortly before the lights and off shortly before they go out.

---

## 12. Settings

The Settings section sits at the very bottom of the page. It holds the names and roles for every output and float — the things you set once during installation and rarely touch again.

### Names

Every output has a **Label**. Changing it renames that output throughout the control panel, so "DC 5" can become "Cooling Fan" and "AC 2" can become "Display Lights". Doser labels also appear as the heading of that doser's own section.

### Mains outlet modes

AC 1 to AC 4 each have a **Mode** — Off, Always On, Scheduled or Heater. See section 11.

### Output roles

Outputs DC 4 to DC 8 can each do one of two jobs. The role decides which.

| Output | Roles available | Default |
|---|---|---|
| DC 4 | Doser / Refill Solenoid | Doser |
| DC 5 | Doser / Cooling Fan | Cooling Fan |
| DC 6 | Doser / CO2 | CO2 |
| DC 7 | Doser / ATO | ATO |
| DC 8 | Doser / ATO Fill | ATO Fill |

DC 3 is always a dosing pump, so it has a label but no role.

### Float roles

**Float 1 Role** and **Float 2 Role** tell the controller what each float switch is watching. See section 9 for the options and what they do.

> **Important** — Changing a role changes what that output does immediately. If a process is running on that output at the time, it stops safely and clears itself.

---

## 13. Troubleshooting

### The control panel will not load

- Check the controller has power.
- Try the IP address from your router instead of `tankcontroller.local`
- If it has lost your WiFi, it creates its **Tank Controller** network again — reconnect to that and redo section 3.

### Top-ups are not happening

- Read the **ATO Status** line. It names the reason directly.
- Check **ATO Enabled** is on.
- If it says `stopped by user`, press Continue.
- If it says `max runtime reached`, the pump ran out of time — check the reservoir has water and the tubing is not blocked, then press Top Up Now.

### A water change stopped part way

- Read **Water Change Status** — it shows whether it is waiting, filling, or paused.
- If paused for a leak, reservoir or drainage container, fix the cause and press Continue.
- To abandon it entirely, press Cancel. You can then start a fresh change.

### A process will not start

Most often another run is still active. Press Cancel for that process, then start it again.

It can also be a role. Automatic reservoir filling needs DC 4 set to Refill Solenoid and Float 2 to Reservoir Full; ATO Fill needs DC 8 set to ATO Fill and Float 1 to ATO Full. Check these in the Settings section.

### A doser section says "Not in Use"

That output is currently set to another job. Open Settings and change that output's Role to **Doser**. Its dosing buttons stay inactive until you do.

### Dosing volumes are wrong

Recalibrate that pump using the steps in section 10. Tubing stiffens with age and delivery rates drift over time — recalibrating every few months is good practice.

### After a power cut

The controller restarts by itself and reconnects to your WiFi. All your settings are kept. If a water change was running when the power failed, it restarts in a paused state so the tank is never left part-drained without you knowing — check Water Change Status and press Continue or Cancel.

> **Leak detected** — If the leak detector triggers, the controller stops all water movement immediately and refuses to start new water changes or top-ups. Find and fix the leak, dry the sensor, then press Continue on whichever process was interrupted.

---

## 14. Quick Reference

| Setting | Default | Range |
|---|---|---|
| Heating target | 25 °C | 15 – 35 °C, 0.5 steps |
| Cooling target | 28 °C | 15 – 35 °C, 0.5 steps |
| Temperature tolerance | 0.3 °C | Fixed |
| ATO Max Runtime | 120 s | 5 – 600 s |
| ATO Fill Max Runtime | 120 s | 5 – 1800 s |
| Reservoir Fill Max Runtime | 300 s | 5 – 3600 s |
| Water Change Drain Time | 300 s | 60 – 3600 s |
| Water Change Fill Ratio | 1.5 | 0.5 – 5.0 |
| Doser volume | 5 mL | 0 – 500 mL |
| Doser rate | 1.6 mL/s | 0.05 – 20 mL/s |
| Flush / calibration time (per doser) | 10 s | 1 – 60 s |

*Access point name: **Tank Controller** · Password: **tankcontroller** · Setup address: **192.168.4.1***
