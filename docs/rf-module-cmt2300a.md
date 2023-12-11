### RF Module CMT2300A

Links to Datasheets, etc. here

Some Closeup Shots of the Circuitry

Some Details about the Software Library

[CMT2300AW_Quick_Start_Guide-Rev0.8](https://github.com/DanielR92/CMT2300A/blob/main/EBYTE/AN142_CMT2300AW_Quick_Start_Guide-Rev0.8.pdf)

[CMT2300AW_RSSI_Usage_Guideline_EN_V0.9](https://github.com/DanielR92/CMT2300A/blob/main/EBYTE/AN144-CMT2300AW_RSSI_Usage_Guideline_EN_V0.9.pdf)

[E49-900M20S-Usermanual_EN](https://github.com/DanielR92/CMT2300A/blob/main/EBYTE/E49-900M20S-Usermanual_EN_v1.0.pdf)


## Software
### CMT2300A
In order to put the module into operation, it is necessary to configure it before use.
Please take the memory table from the datasheet to set the exact desired configuration. To speak to the WR later, a specific configuration must be stored. - The complete information can be found in the "cmt2300a_params.h" file.

### CMT2300AW Register Partition Tab

### Configuration Bank
This bank is used to configure the chip. 
Address: `0x00– 0x5F` 
They include：
1. Reserved attributes for internal use
2. System operation
3. RF characteristics
4. FSK demodulation
5. Clock recovery
6. AGC characteristics
7. OOK demodulation
8. Packet format and codec mode
9. Modulation characteristics of TX 

The value of the register can either come from the RFPDK, or can be changed by the
customer in accordance with their own needs in the application process. In general,
except that the individual register on the RF frequency or data rate may be configured
multiple times in the application, most of the rest of the register only need to be
configured one time in the initialization proce.

### Control Bank 1
Address: `0x60 – 0x6A` 
The bank is used to real-time control the chip. They include:
1. Chip state switch
2. Special function enable
3. Channel switching by hopping manually
4. IO control
5. Interrupt enable
6. FIFO mode configuration
7. Related interrupt control
Control bank 1 can be saved in the SLEEP state. As long as the battery is not powered
down and the chip is not reset, the configuration content will not be lost.

### Control Bank 2
Address: `0x6B – 0x71` 
This bank is provided to the user to control the chip. They include:
1. Packet and FIFO interrupt control
2. FIFO control
3. RSSI read
4. LBD function control
The control bank 2 is not saved in the SLEEP state. All the configured values and the
values that can be read will disappear. Users need to pay attention to it.
