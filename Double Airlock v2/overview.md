# Overview

## Master

1. Int door
2. Ext door
3. Slave
4. Sibling (optional)
5. Override switch

Monitors and controls doors.
Also checks its own Setting to see if it has changed, and if so cycles the airlock.

Controls Slave via commands for depressurizing/pressurizing to/from in- and exterior.

If Sibling is set, the opposite command will be sent to it when cycling.
This will keep one airlock open outwards and one inwards when possible.


## Slave

1. Int vent
2. Ext vent
3. Int sensor
4. Ext sensor
5. Airlock sensor

-  0: Idle
- 10: Depressurize to Exterior
- 11: Depressurize to Interior
- 20: Pressurize from Interior
- 21: Pressurize from Exterior

Commands are received on the Setting parameter.
Resets its Setting back to idle when finished with task.
