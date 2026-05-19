# Bottle Filling Line Simulator

A virtual bottle filling line built on TwinCAT 3 that implements a full PackML unit state machine across three coordinated stations. The project demonstrates how to structure a modular, OOP-based PLC program without requiring any physical hardware, using TwinCAT's virtual runtime to run and observe the simulation entirely on a development PC.

## What This Demonstrates

- PackML unit and module state machines implemented in Structured Text
- Structured Text per IEC 61131-3 including data types, function blocks, and enumerations
- OOP function block design in TwinCAT 3 using EXTENDS and interface patterns
- Virtual runtime simulation — no hardware required
- UML state diagram documentation generated from PlantUML source

## Architecture

The line consists of three stations that each run their own module-level PackML state machine, coordinated by a unit-level state machine:

| Station | Responsibility |
|---------|---------------|
| Infeed Conveyor | Indexes bottles from the infeed queue to the fill position. |
| Fill Station | Dispenses a measured volume of product into each bottle. |
| Capping Station | Places and torques a cap onto each filled bottle. |

## How to Run

**Requirements:** TwinCAT 3.1 XAE Build 4024 or later

1. Clone the repository to a Windows PC with TwinCAT XAE installed.
2. Open the TwinCAT project in TwinCAT XAE (Visual Studio shell).
3. Activate the configuration to deploy to the local runtime.
4. Start the virtual runtime from the TwinCAT toolbar.
5. Set `SC_Reset` to `TRUE` in the watch window to begin the startup sequence.

## Project Status

- [ ] PackML state enum DUT
- [ ] Unit state machine FB
- [ ] Infeed conveyor station FB
- [ ] Fill station FB
- [ ] Capping station FB
- [ ] UML diagrams complete
- [ ] Simulation tested end-to-end
