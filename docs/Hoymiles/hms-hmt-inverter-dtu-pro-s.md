### HMS-/HMT-Inverter and DTU Pro S Details

Links to Whitepapers, FCC IDs and HMS-101 Module Details

Closeup Photos of the open DTU Pro S and HMS-101 Modules without protective metal sheet

Links to several github issues which have so far documented the details


***

1. [CMT2300A RX/TX-Module](https://github.com/lumapu/ahoy/wiki/RF-Module-CMT2300A---E49-900M20S)


# What is the current process flow (comunication between ARM-Chip and CMT2300A)?

After switching on the DTU, the initialization phase starts. This is where configurations in memory are retrieved and sub-areas in the DTU are configured with this information.
A CMT2300A chip is installed in the transmitter and receiver unit. This chip takes on various tasks and has its task in receiving data from the WR (inverter) and forwarding it to the ARM chip. Just as well to send data to the WR, for example to carry out a limitation.

## Hardware
### Original DTU
<coming soon>
