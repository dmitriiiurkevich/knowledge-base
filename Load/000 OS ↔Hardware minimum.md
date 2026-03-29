Timer

CPU

The processor's execution is governed by an external clock. 

The system clock, generates regular *clock pulses* to the processor. → Each *clock pulse*, the processor execute one of *processor instructions*, like this:
- read the contents of memory at location X into register Y
- write the contents of register X into memory at location Y
- write into register X sum of contents of registers X and Y
- ...

*Registers* are the microprocessor's internal storage, used for storing data and performing operations on it. 

The operations performed may cause the processor to stop what it is doing and jump to another *instruction* somewhere else in memory.

The *instructions* have to be fetched from memory as they are executed. 

*Instructions* may themselves reference data within memory and that data must be fetched from memory and saved there when appropriate.

