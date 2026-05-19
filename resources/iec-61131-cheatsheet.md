# IEC 61131-3 Cheat Sheet

## Languages Overview

| Language | Abbreviation | Description |
|----------|-------------|-------------|
| Structured Text | ST | High-level, Pascal-like textual language suited for complex algorithms and calculations. |
| Ladder Diagram | LD | Graphical language derived from relay ladder logic; the most widely used PLC language. |
| Function Block Diagram | FBD | Graphical language based on signal flow between interconnected function blocks. |
| Instruction List | IL | Low-level, assembly-like textual language (deprecated in the third edition). |
| Sequential Function Chart | SFC | Graphical language for sequencing; defines steps, transitions, and actions. |

## Structured Text Syntax Basics

### Variable Declaration

```pascal
VAR
    iCounter  : INT    := 0;
    rSetpoint : REAL   := 100.0;
    bEnabled  : BOOL   := FALSE;
    sLabel    : STRING := 'Line 1';
END_VAR
```

### IF / THEN / ELSE

```pascal
IF bEnabled AND iCounter < iLimit THEN
    iCounter := iCounter + 1;
ELSIF iCounter >= iLimit THEN
    bEnabled := FALSE;
ELSE
    iCounter := 0;
END_IF
```

### CASE Statement

```pascal
CASE eState OF
    STATE_IDLE:
        bReady := TRUE;
    STATE_RUNNING:
        fbProcess();
    STATE_ERROR:
        fbAlarm.Set();
    ELSE
        eState := STATE_IDLE;
END_CASE
```

### FOR Loop

```pascal
FOR i := 0 TO 9 DO
    aBuffer[i] := 0;
END_FOR
```

## Data Types

| Type | Size | Range / Notes |
|------|------|---------------|
| BOOL | 1 bit | TRUE or FALSE |
| INT | 16 bit | −32 768 to 32 767 |
| DINT | 32 bit | −2 147 483 648 to 2 147 483 647 |
| REAL | 32 bit | IEEE 754 single-precision float |
| TIME | 32 bit | Duration literal, e.g. `T#1s500ms` |
| STRING | variable | Default 80 chars; declare as `STRING(n)` for custom length |

## Function Block Structure

```pascal
FUNCTION_BLOCK FB_Example
VAR_INPUT
    bEnable   : BOOL;
    rSetpoint : REAL;
END_VAR
VAR_OUTPUT
    bDone  : BOOL;
    bError : BOOL;
END_VAR
VAR
    fbTimer : TON;
    iStep   : INT := 0;
END_VAR

IF bEnable THEN
    (* implementation *)
END_IF
```
