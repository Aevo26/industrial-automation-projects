# System Architecture

## Station Overview

The bottle filling line is composed of three stations, each modeled as an independent TwinCAT function block with its own module-level PackML state machine:

| Station | Function Block | Responsibility |
|---------|---------------|----------------|
| Infeed Conveyor | FB_InfeedConveyor | Indexes bottles from the infeed queue to the fill position. |
| Fill Station | FB_FillStation | Dispenses a measured volume of product into each bottle. |
| Capping Station | FB_CappingStation | Places and torques a cap onto each filled bottle. |

## State Machine Hierarchy

The system uses a two-level PackML hierarchy:

- **Unit State Machine** — The top-level coordinator (`FB_UnitStateMachine`) aggregates the status of all three module state machines. Unit-level commands (e.g., `SC_Start`) cascade down to each module in the appropriate sequence. The unit reaches `Execute` only when all modules have reached `Execute`.
- **Module State Machines** — Each station function block owns a module-level PackML state machine. A module can transition independently within its own state (e.g., a module may reach `Suspended` without the entire unit suspending), but the unit coordinator enforces line-level interlocks.

## Design Decisions

> _Placeholder — document key design decisions here as they are made, including alternatives considered and the rationale for the chosen approach._
