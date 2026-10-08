# Qidi Q2 – Klipper Configuration & Macros

A complete Klipper setup for the Qidi Q2 without the Qidi Box, built around a normal external filament spool or dry box setup.

This repository brings together the main printer configuration, custom macros, KAMP adaptive bed meshing, Fluidd customisation, and helper files for a more usable Q2 experience without the stock Qidi ecosystem.

---

## Overview

This project exists to make the Qidi Q2 easier to run under Klipper and Fluidd without needing to build everything from scratch.

It includes:

- Main Qidi Q2 `printer.cfg`
- Custom macro configuration in `My_Configs.cfg`
- Additional utility and compatibility macros in `gcode_macro.cfg`
- KAMP adaptive bed meshing and purge setup
- Qidi-specific print/start/end logic and filament routines
- Fluidd console cleaning presets
- Fluidd UI organisation notes
- ORCA slicer machine settings for the print-start and print-end sequences

---

## Important

### This configuration is for a Qidi Q2 WITHOUT the Qidi Box

This setup is intended for a Qidi Q2 running standard Klipper with an external filament setup, not the stock Qidi Box system.

If you are using the Qidi Box, this repository is not intended for your printer setup.

The configuration still contains Qidi-specific compatibility sections where needed, but the custom behaviour and macros in this repository are designed for a more manual, external-filament workflow.

---

## What this project includes

### Main printer configuration

`printer.cfg` includes the core Qidi Q2 configuration:

- CoreXY motion setup
- X/Y/Z steppers and drivers
- Extruder configuration
- Heated bed and chamber control
- Fans and cooling
- Probe and bed mesh configuration
- Input shaping / resonance testing
- Z tilt and tramming configuration
- Filament runout sensor
- Fluidd/Klipper integration
- Included KAMP and custom macro references

### Custom macros

`My_Configs.cfg` contains the main custom automation for the printer, including:

- `PRINT_START`
- `MY_PRINT_END`
- `CANCEL_PRINT`
- `LOAD_FILAMENT`
- `UNLOAD_FILAMENT`
- `SCREWS_TILT`
- `Z_TILT`
- `PID_BED`
- `PID_EXTRUDER`
- `SET_PAUSE_NEXT_LAYER`
- `SET_PAUSE_AT_LAYER`
- `PROBE_BED`
- Lubrication timer and maintenance reminders
- Custom nozzle cleaning and wipe routines
- Filament purge and cleanout behaviours for PLA/PETG and ASA/ABS

### Utility macros

`gcode_macro.cfg` contains the lower-level helper macros for:

- Position parameters
- Homing helpers
- Z offset saving and restoring
- Nozzle clear / wipe / ooze routines
- Move-to-trash positions
- Sensor enable/disable helpers
- Fan and chamber temperature override handling
- Input-shaping and calibration workflows
- Pause/resume behaviour
- Filament load/unload flows
- Cutter and cleaning actions

### KAMP adaptive bed meshing

The repository includes KAMP support for adaptive mesh generation instead of probing the full bed every print.

Included files:

- `KAMP/Adaptive_Meshing.cfg`
- `KAMP/KAMP_Settings.cfg`
- `KAMP/Line_Purge.cfg`

KAMP features included here:

- Adaptive mesh generation around printed objects
- Smart park support
- Line purge support
- Reduced probing time on normal prints
- Full-bed mesh option still available

Important requirements for KAMP:

1. `Adaptive_Meshing.cfg` is loaded.
2. No conflicting `BED_MESH_CALIBRATE` macro overrides KAMP.
3. `[exclude_object]` is enabled in the slicer.
4. The slicer provides object information for adaptive mesh calculation.

---

## Bed mesh and probing setup

The configuration uses a full bed mesh range of:

- X: 10 – 260 mm
- Y: 10 – 260 mm

Default mesh:

- 9 × 9 probe grid

Mesh algorithm:

- Bicubic

This allows:

- Full-bed mesh when needed
- KAMP adaptive mesh as the normal print workflow

---

## Print process and workflow

The general workflow in this repo is:

1. Backup current configuration.
2. Install the supplied files.
3. Ensure the printer.cfg includes the correct macros and KAMP files.
4. Restart Klipper.
5. Check homing, movement, temperatures, probe, bed mesh, Z tilt, and filament sensor.
6. Start printing with the configured print-start sequence.

The print-start logic includes:

- Homing
- Chamber heating
- Bed heating
- Z offset reset
- Nozzle cleaning
- Z tilt adjust
- Adaptive bed mesh
- Temperature waits
- KAMP purge line

The print-end logic includes:

- Cooling and heater shutdown
- Z offset save
- Lubrication timer update
- Sensor disable
- Mesh clear
- Print status reset

---

## Filament functions

The repo includes multiple filament workflows for different material types.

### Loading

Examples include:

- `LOAD_FILAMENT`
- `LOAD_FILAMENT_PLA_PETG`
- `LOAD_FILAMENT_PETG_PLA`
- `LOAD_FILAMENT_ASA_ABS`

These are designed around using a dry box or external spool system instead of the Qidi Box.

### Unloading

Examples include:

- `UNLOAD_FILAMENT`
- `UNLOAD_FILAMENT_PLA_PETG`
- `UNLOAD_FILAMENT_ASA_ABS`

These include extra heat and cleaning routines for different filament classes.

### Pause at layer

Examples:

- `SET_PAUSE_NEXT_LAYER`
- `SET_PAUSE_AT_LAYER LAYER=37`

This is useful for inspection or mid-print intervention.

---

## Nozzle cleaning and maintenance

The repo contains custom nozzle cleaning routines tailored to the Qidi Q2’s nozzle cleaning area.

Included routines:

- `CLEAR_NOZZLE`
- `CLEAR_NOZZLE_PLR`
- `SHAKE_OOZE`
- `MOVE_TO_TRASH`

These are integrated into print preparation, filament loading, unloading, and maintenance routines.

The project also includes a maintenance timer sequence:

- print time reminder before lubrication work is recommended
- current setup: approx. 30 hours of print time before reminder

---

## Fluidd and console setup

Recent additions to the repository include a series of Fluidd-specific helper files and workflow notes.

### `FLUIDD UI Setup`

This guide explains how to:

- back up the existing Klipper configuration
- rename original files
- install the supplied KAMP and macro files
- organise macros into categories in Fluidd
- use the bed screw adjustment macros and Z tilt routine

### `Clean up the Fluidd Console`

This file explains how to add console filters to hide noisy metadata and probe messages, keeping the console readable and focused on useful output.

### `Fluidd-Settings-Backup.json`

This is a saved Fluidd settings export that can be imported into a Fluidd installation to restore the cleaner console view and configured layout.

---

## ORCA slicer settings

The repository also includes a file for ORCA slicer machine settings:

- `ORCA machine settings sept 2026`

This contains example print-start and print-end G-code based on the macros in this setup, including:

- `PRINT_START` usage
- `SET_PRINT_STATS_INFO`
- `M140`, `M104`, `M141`
- chamber and bed temperature handling
- adaptive mesh start sequence
- `MY_PRINT_END`
- `UNLOAD_FILAMENT`
- layer-change and pause handling

This is useful if you are slicing with ORCA and want the print routine to match the macros and setup in this repo.

---

## Files in this repository

The repository currently contains:

- `printer.cfg`
- `My_Configs.cfg`
- `gcode_macro.cfg`
- `KAMP/Adaptive_Meshing.cfg`
- `KAMP/KAMP_Settings.cfg`
- `KAMP/Line_Purge.cfg`
- `FLUIDD UI Setup`
- `Clean up the Fluidd Console`
- `Fluidd-Settings-Backup.json`
- `ORCA machine settings sept 2026`
- `README.md`

---

## Recommended installation process

1. Back up your existing configuration.
2. Rename existing files before replacing them.
3. Upload the supplied files into your Klipper config directory.
4. Make sure `printer.cfg` includes the correct files.
5. Restart Klipper.
6. Check the console for errors.
7. Verify:
   - homing
   - X/Y/Z movement
   - probe operation
   - bed mesh
   - screw tilt
   - Z tilt
   - extruder and heater function
   - fans
   - filament sensor
8. Import the Fluidd console settings if desired.
9. Use the ORCA machine settings if you are slicing with ORCA.

---

## A note about the original Qidi config

This project does not try to replace every Qidi OEM part of the printer setup.

Instead, it keeps useful Qidi-specific compatibility sections and combines them with custom Klipper functionality to create a practical, working configuration for a Qidi Q2 without the Qidi Box.

---

## Important warnings

These configuration files contain Qidi-specific movement coordinates, macro timings, temperatures, and hardware assumptions.

They should not be treated as a universal Klipper configuration.

If your printer has been modified or you have custom hardware changes, some values may need adjustment.

Always check movement, temperature stability, nozzle wiping, and bed mesh behaviour after installing a new configuration.

---

## Disclaimer

Use these files at your own risk.

Always keep a backup of your original Qidi configuration before making changes.

The author accepts no responsibility for damage to the printer, hotend, heated bed, electronics, or other equipment caused by using these configuration files or macros.

---

## Project goal

The goal of this project is to make the transition to a more custom Klipper and Fluidd workflow on the Qidi Q2 as straightforward as possible.

Instead of spending time figuring out which macros are needed, where they belong, and how KAMP and Qidi-specific functionality should be combined, this repository provides a ready-to-use base for a working setup without the Qidi Box.

Copy, configure, check, and print.

---

## Quick start summary

If you want the short version:

- This is a Qidi Q2 Klipper config for non-Qidi-Box setups.
- It includes custom macros, KAMP adaptive meshing, and Fluidd tuning.
- It has support for external filament spool or dry box workflows.
- It also includes custom console filters and ORCA settings to make the workflow smoother.

This repository is built to give you a practical starting point rather than a generic printer config.

