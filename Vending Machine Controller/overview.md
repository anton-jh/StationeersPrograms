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
1. "Slave"
2. Dial
3. Button
4. Display
5. Vending Machine (for counting inventory when needed)
6. Sorter (for counting imported stacks)

Keeps track of types and quantities.
Counts imported stacks.
Sends commands to "Slave" to vend or defrag.

Format in stack memory:
    0. Hash 1
    1. Quantity 1
    2. Hash 2
    3. Quantity 2
    ...


### Slave

1. Vending Machine
2. Stacker
3. Sorter
4. Silo (return)
5. Silo (import)

Takes requests via its Setting parameter.
    If Setting = 1, Silo (import) will be closed.
    Otherwise, parse as following:
    `hash + amount / 1000` where `0 <= amount <= 999`
        If `amount` is 0, the requested type will be defragmented.
        Otherwise the amount will be sent to output.
    To decode: `hash = truncate(raw)`, `amount = (raw - hash) * 1000`

Resets its Setting parameter to 0 when done and ready for new request.
