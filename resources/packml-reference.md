# PackML Reference

OMAC PackML (Packaging Machine Language), standardized as IEC TR 88-00-02, defines a common state machine model and data model for packaging machines and other industrial automation equipment. It provides a consistent framework for machine states, commands, and modes that enables interoperability between machines from different vendors and simplifies integration into MES and SCADA systems.

## States

### Stable States

| State | Description |
|-------|-------------|
| Stopped | Machine is powered and stationary; all motion has ceased and the machine is ready to be reset. |
| Idle | Machine has been reset and is ready to accept a Start command. |
| Suspended | Machine has paused execution due to an upstream or downstream process condition. |
| Execute | Machine is actively running and producing. |
| Held | Machine has been temporarily paused by an operator-initiated Hold command. |
| Complete | The current production run has finished normally. |
| Aborted | Machine has entered a safe, de-energized state after an Abort command or fault. |

### Acting States

| State | Description |
|-------|-------------|
| Resetting | Machine is executing the reset sequence, transitioning toward Idle. |
| Starting | Machine is executing the start sequence, transitioning toward Execute. |
| Completing | Machine is executing end-of-run procedures, transitioning toward Complete. |
| Stopping | Machine is executing the stop sequence, transitioning toward Stopped. |
| Holding | Machine is executing the hold sequence, transitioning toward Held. |
| UnHolding | Machine is executing the unhold sequence, transitioning toward Execute. |
| Suspending | Machine is executing the suspend sequence, transitioning toward Suspended. |
| UnSuspending | Machine is executing the unsuspend sequence, transitioning toward Execute. |
| Aborting | Machine is executing emergency shutdown procedures, transitioning toward Aborted. |
| Clearing | Machine is executing the clear sequence, transitioning toward Stopped. |

## Commands

| Command | Description |
|---------|-------------|
| SC_Reset | Transitions the machine from Stopped or Complete to the Resetting acting state. |
| SC_Start | Transitions the machine from Idle to the Starting acting state. |
| SC_Stop | Initiates an orderly stop, transitioning to the Stopping acting state from most stable states. |
| SC_Hold | Pauses execution from Execute, transitioning to the Holding acting state. |
| SC_UnHold | Resumes execution from Held, transitioning to the UnHolding acting state. |
| SC_Suspend | Pauses execution due to an external condition, transitioning from Execute to Suspending. |
| SC_UnSuspend | Resumes execution after the external condition clears, transitioning from Suspended to UnSuspending. |
| SC_Abort | Initiates an immediate safe shutdown; valid from any state, transitioning to Aborting. |
| SC_Clear | Clears the aborted condition and transitions from Aborted to the Clearing acting state. |

## State Transition Rules

- Commands are only accepted in stable states; acting states run to completion autonomously before accepting new commands.
- Acting states self-transition on completion — once the acting state logic finishes, the machine advances to its target stable state without an additional command.
- The Abort command is valid from any state, immediately interrupting any in-progress acting sequence and driving the machine to the Aborted stable state.
