# Qidi Q2 – Klipper Config & Macros

A practical Klipper setup for a Qidi Q2 running without the Qidi Box.

This repo is designed to make a Qidi Q2 easier to run with Fluidd and Klipper using a normal external spool or dry box setup.

It includes a working printer config, custom macros, KAMP adaptive bed meshing, filament routines, nozzle cleaning, pause controls, and Fluidd helpers.

---

## Important

This configuration is for the Qidi Q2 without the Qidi Box.

If you have the Qidi Box installed, this setup is not intended for you.

This project keeps the useful Qidi-compatible parts where needed, but the main goal is a simpler external-filament Klipper workflow.

---

## What’s in this repo

- `printer.cfg` – main Qidi Q2 Klipper configuration
- `My_Configs.cfg` – main custom print, filament, and calibration macros
- `gcode_macro.cfg` – helper macros for homing, offsets, cleaning, pause/resume, and more
- `KAMP/Adaptive_Meshing.cfg` – adaptive bed mesh support
- `KAMP/KAMP_Settings.cfg` – KAMP settings
- `KAMP/Line_Purge.cfg` – purge line support
- `FLUIDD UI Setup` – basic install and layout guide
- `Clean up the Fluidd Console` – console filters to reduce noise
- `Fluidd-Settings-Backup.json` – saved Fluidd console settings
- `ORCA machine settings sept 2026` – ORCA print start/end G-code examples

---

## Main features

- Print start sequence with bed heat, chamber heat, homing, cleaning, Z tilt, and adaptive mesh
- Print end routine with heater shutoff, mesh clear, and status reset
- Filament load and unload macros for common materials
- Nozzle cleaning and wipe routines
- Pause-at-layer support
- PID tuning macros for bed and hotend
- Z offset handling
- Bed screw adjustment and Z tilt setup
- KAMP adaptive bed meshing
- Lubrication reminder timer
- Fluidd console cleanup options

---

## Bed mesh and KAMP

This setup uses a 9x9 full-bed probe area with:

- X: 10–260 mm
- Y: 10–260 mm

KAMP is included so you can do adaptive mesh instead of probing the whole bed every print.

KAMP works best when:

1. `Adaptive_Meshing.cfg` is included
2. There is no conflicting `BED_MESH_CALIBRATE` macro
3. `[exclude_object]` is enabled in the slicer
4. The slicer provides object information for adaptive meshing

---

## Typical workflow

1. Back up your current config
2. Rename your original files as a backup
3. Copy these config files into your Klipper config folder
4. Check the includes in `printer.cfg`
5. Restart Klipper
6. Check these before printing:
   - homing
   - X/Y/Z movement
   - probe operation
   - bed mesh
   - Z tilt
   - screw tilt
   - extruder and heaters
   - fans
   - filament sensor

---

## Filament macros

Examples included:

- `LOAD_FILAMENT`
- `LOAD_FILAMENT_PLA_PETG`
- `LOAD_FILAMENT_PETG_PLA`
- `LOAD_FILAMENT_ASA_ABS`
- `UNLOAD_FILAMENT`
- `UNLOAD_FILAMENT_PLA_PETG`
- `UNLOAD_FILAMENT_ASA_ABS`

These are designed around external filament handling and a dry box or normal spool setup.

---

## Nozzle cleaning and maintenance

This repo includes custom nozzle cleaning routines for the Qidi Q2, such as:

- `CLEAR_NOZZLE`
- `CLEAR_NOZZLE_PLR`
- `SHAKE_OOZE`
- `MOVE_TO_TRASH`

A maintenance reminder timer is also included, with the current default set to trigger after around 30 hours of print time.

---

## Fluidd setup

The repo includes extra notes and settings for making Fluidd easier to use:

- categorize macros in the UI
- clean up noisy console output
- import a saved console filter config
- keep the printer interface less cluttered

Use the files:

- `FLUIDD UI Setup`
- `Clean up the Fluidd Console`
- `Fluidd-Settings-Backup.json`

---

## ORCA slicer support

The repo also includes example ORCA machine settings for print start/end G-code:

- `ORCA machine settings sept 2026`

This is useful if you want your slicer to match the same start/end logic used by this config.

---

## Important notes

These configs are Qidi Q2 specific.

They include hardware-specific coordinates, temperatures, and macro behavior. They are not a generic Klipper config for all printers.

If you changed your hardware or setup, some settings may need adjusting.

---

## Disclaimer

Use these files at your own risk.

Always keep a backup of your original Qidi configuration before changing anything.

The author accepts no responsibility for damage caused by using these configuration files or macros.

---

## Project goal

This project aims to make switching a Qidi Q2 to a custom Klipper/Fluidd setup as easy as possible without needing to build everything from scratch.

Instead of figuring out the macros, KAMP setup, and Qidi compatibility pieces one by one, this repo gives you a ready-to-use base.

Copy, configure, check, and print.
