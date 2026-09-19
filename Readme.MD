# Redes Automotivas - CARLA CAN Networks

This repository contains an academic automotive networks project built around
CARLA and a virtual CAN bus. Its main component is the `yes-carla-can/`
platform, which extends the CARLA driving simulator with SocketCAN traffic,
DBC-based message encoding, attack injection, traffic analysis, and intrusion
detection experiments.

The repository also includes reports, figures, logs, and Overleaf source files
for the project stages.

## Project Overview

The project studies CAN network behavior in a simulated vehicle environment.
It uses CARLA to run a vehicle simulation and Linux SocketCAN (`vcan0`) to
represent the in-vehicle CAN bus. Vehicle control messages are encoded from DBC
files and published to the virtual bus, while attack and defense modules can
inject malicious traffic or detect anomalous behavior.

The experiments cover:

- Virtual CAN communication with CARLA.
- Custom DBC message definitions.
- Normal CAN traffic capture and statistical analysis.
- Spoofing and fuzzy CAN message attacks.
- Intrusion detection based on CAN ID timing behavior.
- Report generation with tables, plots, and experiment evidence.

## Repository Structure

```text
.
+-- yes-carla-can/                  # Main CARLA + CAN simulation platform
|   +-- CARLA_client_module.py       # Connects to CARLA and receives CAN state
|   +-- vehicle_controls_module.py   # Publishes vehicle control frames to vcan0
|   +-- cyberattacks_module.py       # Runs CAN spoofing, fuzzy, and DoS attacks
|   +-- intrusion_detection_module.py # Runs intrusion detection algorithms
|   +-- attacks/                     # Attack implementations
|   +-- can_network/                 # DBC and SocketCAN abstraction layer
|   +-- defense/                     # IDS implementations
|   +-- data/                        # DBC files, captures, analyzers, outputs
|   +-- docs/                        # Stage-specific execution guides
|   +-- gui/                         # CARLA HUD and CAN traffic visualization
|   +-- logs/                        # Captured traffic, analysis outputs, plots
|   +-- sensors/                     # CARLA sensor wrappers
|   +-- tests/                       # Pytest test suite
|
+-- overleaf_etapa3/                 # Report artifacts for stage 3
+-- overleaf_etapa4/                 # Report artifacts for stage 4
+-- overleaf_etapa5/                 # Report artifacts for stage 5
+-- Relatorio_Etapa3_G7.tex          # Stage 3 LaTeX report
+-- Relatorio_Etapa2_G7.pdf          # Stage 2 report
+-- Especificacao Atividade 2 ...    # Assignment specification document
```

## Main Platform

The main platform is available in:

```bash
cd yes-carla-can
```

See [`yes-carla-can/README.md`](yes-carla-can/README.md) for the full platform
documentation, including architecture, installation, dependency details, and
experiment reproduction steps.

Core scripts:

- `0_install_dependencies.sh` installs system packages, Python dependencies,
  Miniconda support if needed, and CARLA 0.9.15.
- `1_up_environment.sh` starts CARLA, configures the virtual CAN interface, and
  launches the simulation modules.
- `2_down_environment.sh` stops the simulation environment.

## Requirements

The project is intended for Linux systems with SocketCAN support. The tested
environment uses:

- Ubuntu/Debian-based Linux.
- Python 3.9 through the `n4s_env` conda environment.
- CARLA 0.9.15.
- SocketCAN and `can-utils`.
- Python packages listed in `yes-carla-can/requirements.txt`.

CARLA is large and GPU-sensitive, so make sure the machine has enough disk
space and graphics support before running the full simulator.

## Quick Start

From the main platform directory:

```bash
cd yes-carla-can
./0_install_dependencies.sh
./1_up_environment.sh
```

To use the custom DBC from the project stages:

```bash
./1_up_environment.sh --dbc data/our_dbcfile.dbc
```

When finished:

```bash
./2_down_environment.sh
```

## Experiments and Documentation

Stage-specific guides are stored in `yes-carla-can/docs/`:

- `etapa3.md`: CAN traffic capture and statistical analysis.
- `etapa4.md`: CAN message manipulation and visual impact analysis.
- `etapa5.md`: Intrusion detection experiments and detector improvement.

Generated logs, CSV files, JSON statistics, and plots are stored under
`yes-carla-can/logs/` and `yes-carla-can/data/`.

## Tests

The `yes-carla-can/tests/` directory contains automated tests for DBC loading,
message encoding, CAN network behavior, traffic analysis, and intrusion
detection logic.

Run them from the platform directory:

```bash
cd yes-carla-can
pytest
```

## Reports

The `overleaf_etapa*/` directories contain LaTeX sources, figures, and PDFs used
for the written reports. They document the experimental procedure and results
for each stage of the project.

## License

The main platform includes its own license file at
`yes-carla-can/LICENSE`.
