# Overview


## ICs

### Master

1. Door Int A
2. Door Int B
3. Door Ext A
4. Door Ext B
5. Override Switch A
6. Override Switch B

mode: 0=a to int, 1=b to int


### SlaveA

1. IC Housing Master
2. Active Vent Int A
3. Active Vent Int B
4. Active Vent Ext A
5. Active Vent Ext B


110+mode for depressurizing
120+mode for pressurizing

- 100: All vents off
- 110: A to Ext, B to Int
- 111: A to Int, B to Ext
- 120: Int to A, Ext to B
- 121: Ext to A, Int to B

Other values are ignored.


### SlaveB

1. IC Housing Master
2. Gas Sensor Int
3. Gas Sensor Ext
4. Gas Sensor A
5. Gas Sensor B


- 100: Idle
- 110,111: Report if both are depressurized
- 120: Report if A gt Int and B gt Ext
- 121: Report if A gt Ext and B gt Int

All checks will return either 0 or 1 as Setting.
Will remember last valid request and continuosly update Masters Setting.
