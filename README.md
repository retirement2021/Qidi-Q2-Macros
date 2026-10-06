# Qidi-Q2
Qidi Q2  Without a Qidi Box, Macros and adaptive bed mesh
# Qidi Q2 – Klipper Configuration & Macros

A complete set of custom Klipper configuration and macros for the **Qidi Q2 without the Qidi Box**.

Qidi Q2, configs, macros, 3D printer, Klipper, firmware, settings, printer configuration

The aim of this project is simple:

**To provide Qidi Q2 owners who are running without a Qidi Box with a ready-to-use Klipper configuration, rather than requiring them to build and modify the configuration themselves.**

This configuration brings together the main printer configuration, custom macros, KAMP adaptive bed meshing and a number of useful Klipper/Fluidd functions into one working setup.

---

## ⚠️ Important

### This configuration is for a Qidi Q2 WITHOUT the Qidi Box

These files have been developed around a Qidi Q2 being used with a **normal external filament spool or dry boxes** rather than the Qidi Box.

If you have a Qidi Box installed, this is **not intended for you**.

The configuration contains some original Qidi code and compatibility sections because they form part of the Q2's normal Klipper environment. However, the custom functionality in this repository is primarily aimed at the **non-Qidi-Box Q2**.

---

# What This Project Provides

The intention is to give a Qidi Q2 owner a well-rounded Klipper/Fluidd setup with minimal configuration work.

The package includes:

* Main Qidi Q2 `printer.cfg`
* Custom macro configuration
* Custom print-start sequence
* Custom print-end functions
* KAMP adaptive bed meshing
* Full 9 × 9 bed probing
* Nozzle cleaning routines
* Filament loading and unloading
* Filament runout handling
* Pause-at-layer functions
* PID tuning macros
* Z-offset handling
* Resonance testing configuration
* Z-tilt adjustment
* Bed mesh configuration
* Useful Fluidd controls and status functions
* Qidi-specific compatibility macros
* Various convenience and maintenance macros

---

# Files

The repository contains four main configuration files.

├── printer.cfg
├── My_Configs.cfg
├── gcode_macro.cfg
└── KAMP/
    └── Adaptive_Meshing.cfg


## `printer.cfg`

The main Qidi Q2 Klipper configuration.

This contains the printer's:

* CoreXY motion system
* X, Y and Z steppers
* TMC motor drivers
* Extruder
* Hotend
* Heated bed
* Chamber heater
* Fans
* Probe
* Filament sensor
* Accelerometer
* Bed mesh
* Z tilt
* Resonance testing
* Save variables
* Klipper/Fluidd configuration

It also contains the required includes for the custom configuration and KAMP.

---

## `My_Configs.cfg`

This is the main collection of **custom macros and modifications**.

It contains many of the functions that make this configuration different from the standard Qidi setup.

Examples include:

### Print Start

A customised `PRINT_START` sequence handling:

* Homing
* Loading the filament
* Unloading the filament
* Bed heating
* Chamber heating
* Z offset
* Nozzle cleaning
* Screws_Tilt
* Z tilt
* Adaptive bed meshing
* Nozzle temperature
* Filament sensing
* Print preparation

---

### Filament Loading

Custom filament-loading macros provide simple options for different filament situations.

Examples include:

```text
LOAD_FILAMENT
LOAD_FILAMENT_20mm purge
LOAD_FILAMENT_45mm purge
LOAD_FILAMENT_ASA_ABS a hotter 45mm perge
```

These are designed around using an **external filament spool or dry boxes**, rather than requiring the Qidi Box.

---

### Filament Unloading

Custom unload functions are also provided, including a higher-temperature unload option for materials such as ASA/ABS.

---

### Pause at Layer

The configuration includes custom layer-pause controls.

For example:

```gcode
SET_PAUSE_NEXT_LAYER
```

or:

```gcode
SET_PAUSE_AT_LAYER LAYER=37
```

This allows a print to be paused automatically at a chosen layer.

---

### PID Tuning

Simple macros are provided for PID tuning.

For example:

```gcode
PID_BED TARGET_TEMP=60
```

and:

```gcode
PID_EXTRUDER TARGET_TEMP=235
```

---

### Bed Probing

A custom:

```gcode
PROBE_BED
```

macro is included for performing a full bed calibration.

The routine heats the bed, cleans the nozzle, performs a **9 × 9 bed mesh**, saves the resulting mesh and returns the printer to a safe position.

---

# `gcode_macro.cfg`

This file contains additional Qidi Q2 macros and supporting functions.

Among other things, it provides:

* Printer position parameters
* Homing helper
* Z-offset functions
* Nozzle cleaning
* Nozzle wiping
* Ooze clearing
* Move-to-trash position
* Filament extrusion/flush functions
* Sensor enable/disable
* Qidi-compatible commands
* Printer utility functions

The macros use Qidi Q2-specific positions and hardware, so this file should be regarded as **Qidi Q2 specific** rather than a generic Klipper macro collection.

---

# KAMP Adaptive Meshing

The included `Adaptive_Meshing.cfg` provides adaptive bed meshing.

Instead of probing the entire bed for every print, KAMP examines the objects in the G-code and calculates the area that needs to be probed.

The mesh is therefore concentrated around the actual print area.

The configuration also includes:

```ini
[exclude_object]
```

which is required for the adaptive mesh calculation.

### Requirements

For adaptive meshing to work correctly:

1. `Adaptive_Meshing.cfg` must be loaded.
2. There must not be another active `BED_MESH_CALIBRATE` macro overriding it.
3. `[exclude_object]` must be enabled within the slicer.
4. The slicer must provide the required object information.

---

# Bed Mesh

The Qidi Q2 configuration uses a maximum bed mesh area of:

X: 10 – 260 mm
Y: 10 – 260 mm


with a default:

9 × 9
probe grid.

The configuration uses the bicubic bed-mesh algorithm.

A full-bed mesh can therefore be generated when required, while KAMP can be used for normal prints.

---

# Nozzle Cleaning

The configuration contains custom nozzle-cleaning routines specifically designed around the Qidi Q2's nozzle-cleaning area.

These include:

CLEAR_NOZZLE
CLEAR_NOZZLE_PLR
SHAKE_OOZE
MOVE_TO_TRASH

The cleaning sequence is incorporated into the print preparation process.

Because the movements are based on the physical Qidi Q2, these macros should **not be copied to another printer without checking the coordinates first**.


# Using the Configuration

The intention is that a Qidi Q2 owner without a Qidi Box can use these files as a starting point rather than having to create all of the macros and configuration manually.

### Recommended approach

**1. Back up your existing configuration**

Always make a complete backup before replacing any Klipper configuration files.

**2. Copy the required configuration files**
rename your.cfg files with -original at the end for id

Place the supplied files into your Klipper configuration directory.

**3. Check the includes**

Make sure `printer.cfg` points to the supplied custom configuration and KAMP files.

**4. Restart Klipper**

After installing the files, perform a Klipper restart and check the console for configuration errors.

**5. Check the printer before printing**

Verify:

* Homing
* X/Y/Z movement
* Probe operation
* Bed mesh
* screw_tilt
* Z tilt
* Extruder
* Nozzle cleaning
* Fans
* Heaters
* Filament sensor

Do this before starting a print.

---

# A Note About the Qidi Original Configuration

This project does not attempt to reinvent every part of the Qidi Q2 Klipper configuration.

Where appropriate, Qidi's original configuration and macros are retained and combined with custom Klipper functionality.

The purpose is to provide a **practical, working configuration for the Q2 without the Qidi Box**, while retaining the useful parts of the original Qidi environment.

---

# Important

These configuration files contain **Qidi Q2-specific hardware settings, movement coordinates and macro behaviour**.

They should not be considered a generic Klipper configuration.

If you have modified your Q2 hardware, some settings may need to be adjusted for your particular machine.

Always check the printer's movement and heater behaviour after installing a new configuration.

---

# Disclaimer

Use these files at your own risk.

Always keep a backup of your original Qidi configuration.

The author accepts no responsibility for damage to the printer, hotend, heated bed, electronics or other equipment resulting from the use of these configuration files or macros.

---

## Project Goal

The goal of this project is to make the transition to a more customised Klipper/Fluidd experience on a **Qidi Q2 without the Qidi Box** as straightforward as possible.

Instead of spending time working out which macros are required, where they belong, how KAMP needs to be configured and how the various Qidi functions fit together, this repository provides the configuration as a starting point.

**Copy, configure, check and print.**




