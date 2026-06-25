# PLC Tag Map — AI-ElevatorControl

## Physical Input Bits
| Tag | Physical | Description |
|-----|----------|-------------|
| `Call_MainFloor` | `_IO_EM_DI_00` | Main floor Shelly relay |
| `Call_Basement` | `_IO_EM_DI_01` | Basement Shelly relay |
| `Call_ElevatorCar` | `_IO_EM_DI_02` | In-car Shelly relay |
| `LS_Up` | `_IO_EM_DI_03` | Up limit switch (NC) |
| `LS_Down` | `_IO_EM_DI_04` | Down limit switch (NC) |

## Physical Output Bits
| Tag | Physical | Description |
|-----|----------|-------------|
| `Pump_Up` | `_IO_EM_DO_00` | Hydraulic pump up |
| `Pump_Down` | `_IO_EM_DO_01` | Hydraulic pump down |

## Internal Position Bits
| Tag | Type | Description |
|-----|------|-------------|
| `Pos_AtTop` | BOOL | Elevator at top (derived from LS_Up) |
| `Pos_AtBottom` | BOOL | Elevator at bottom (derived from LS_Down) |
| `Pos_InMiddle` | BOOL | Elevator between floors |

## Internal Motion Bits
| Tag | Type | Description |
|-----|------|-------------|
| `Motion_Up` | BOOL | Elevator moving up |
| `Motion_Down` | BOOL | Elevator moving down |

## Request Bits
| Tag | Type | Description |
|-----|------|-------------|
| `Request_Up` | BOOL | Request to move up |
| `Request_Down` | BOOL | Request to move down |

## Communications
| Tag | Type | Description |
|-----|------|-------------|
| `Heartbeat` | BOOL | Pi writes TRUE every second |
| `Heartbeat_Last` | BOOL | Previous heartbeat state for edge detection |
| `Comms_Fault` | BOOL | Set if heartbeat lost beyond timeout |
| `Comms_OK` | BOOL | NC of Comms_Fault |

## Timers
| Tag | Type | Preset | Description |
|-----|------|--------|-------------|
| `TMR_Heartbeat` | TON | 1000ms | Heartbeat monitor |
| `TMR_Comms_Fault` | TON | 5000ms | Delay before declaring comms fault |
| `TMR_Direction_Change` | TON | 5000ms | Delay between direction changes |

## Program Structure
| Routine | Description |
|---------|-------------|
| Routine 1 | I/O Mapping — physical to internal bits |
| Routine 2 | Position Logic — derive position from limit switches |
| Routine 3 | Call Logic — normal and fallback operation |
| Routine 4 | Safety Interlocks — limits and mutual exclusion |
| Routine 5 | Output Mapping — internal bits to physical outputs |

## Fallback Behavior (Comms_Fault active)
- Car call reverts to shuttle behavior
- At bottom → go up
- At top → go down
- In middle → continue to nearest limit, reverse on next call
- Floor call buttons (I:0, I:1) unaffected and fully operational