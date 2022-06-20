# Overview


## Machines and chutes

- Vending Machine(out) to Stacker(in)
- Stacker(out) to Junction(A)
- Chute Bin(out) to Junction(B)
- Junction(out) to Sorter(in)
- Sorter(A) to Chute Outlet(in)
- Sorter(B) to Silo(in)
- Silo(out) to Vending Machine(in)



## ICs

### Master
1. "Vendor"
2. Dial
3. Button
4. Display                      TODO: How to get values here?
5. Lever (for defragmentation)
6. "Manager"

Sends commands to "Vendor" and "Manager".


### Vendor

1. Vending Machine
2. Stacker
3. Sorter

Takes requests via its Setting parameter.
    Format: `hash + amount / 1000` where `0 <= amount <= 999`
        If `amount` is 0, a "raw" stack from the vending machine will be sent as-is to the Silo.        NOPE!
        Otherwise a stack of `amount` will be sent to the Chute Outlet and any leftovers to the Silo.
    To decode: `hash = truncate(raw)`, `amount = (raw - hash) * 1000`

Resets its Setting parameter to 0 when done and ready for new request.


### Manager

1. Vending Machine
2. Stacker
3. Sorter
4. Silo (defrag)
5. Silo (import)

Will count and keep track of stacks and also perform defragmentation.

Takes commands via its Setting parameter.
    0 = Accept input via Chute Bin.
        - Chute Bin unlocked.
        - Silo open.
    1 = Lock.
        - Chute Bin locked.
        - Silo open.
    2 = Start defragmentation and re-counting. (Will reset Setting to 0 when done.)
