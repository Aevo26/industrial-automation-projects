# PackML State Machine

PackML (Packaging Machine Language), standardized as IEC TR 88-00-02, defines a hierarchical state machine model that provides a consistent control framework across packaging and process equipment. Each machine or module exposes a defined set of stable and acting states, transitions driven by a small command set, and a mode manager for switching between production, maintenance, and manual operating modes.

## States

### Stable States

| State | Description |
|-------|-------------|
| Stopped | Machine is powered and stationary; awaiting a Reset command. |
| Idle | Machine has been reset and is ready to start. |
| Suspended | Execution paused due to an upstream or downstream process condition. |
| Execute | Machine is actively running and producing. |
| Held | Execution temporarily paused by an operator Hold command. |
| Complete | Production run finished normally; awaiting Reset or Stop. |
| Aborted | Machine in a safe, de-energized state following an Abort or fault. |

### Acting States

| State | Description |
|-------|-------------|
| Resetting | Executing reset sequence toward Idle. |
| Starting | Executing start sequence toward Execute. |
| Completing | Executing end-of-run procedures toward Complete. |
| Stopping | Executing stop sequence toward Stopped. |
| Holding | Executing hold sequence toward Held. |
| UnHolding | Executing unhold sequence toward Execute. |
| Suspending | Executing suspend sequence toward Suspended. |
| UnSuspending | Executing unsuspend sequence toward Execute. |
| Aborting | Executing emergency shutdown toward Aborted. |
| Clearing | Executing clear sequence toward Stopped. |

## Commands

| Command | Effect |
|---------|--------|
| SC_Reset | Transitions from Stopped or Complete → Resetting. |
| SC_Start | Transitions from Idle → Starting. |
| SC_Stop | Initiates orderly stop from most stable states → Stopping. |
| SC_Hold | Pauses Execute → Holding. |
| SC_UnHold | Resumes from Held → UnHolding. |
| SC_Suspend | Pauses Execute due to external condition → Suspending. |
| SC_UnSuspend | Resumes from Suspended → UnSuspending. |
| SC_Abort | Valid from any state; immediately drives machine → Aborting. |
| SC_Clear | Clears aborted condition → Clearing → Stopped. |
