
Peripherals are controlled by controller chips on the system board or on cards plugged into it.

The *controllers* 
- are lightweight processors — like the CPU itself — they usually possess their own *controlling registers* which control them,
- are connected to the CPU and to each other by a variety of buses.

Software running on the CPU must be able to read and write those *controlling registers*.

Each controller on a *system bus* has the individually memory space, addressed by the CPU. This is so that the software driver can write to controller registers and thus manipulate the device. 

The *I/O space memory* — memory space that the hardware peripherals exist in.

|                                   | CPU    | I/O controllers                                                            |
| --------------------------------- | ------ | -------------------------------------------------------------------------- |
| access to the system space memory | direct | indirect, only with the help of the CPU                                    |
| access to the I/O space memory    | direct | direct, but only the address space that its *controlling registers* are in |

Typically a CPU will have separate instructions for accessing 
- the system memory space: 
	- read a value from memory address 0x7ffe5367e044 into register X
- the I/O memory space: 
	- read a byte from I/O address 0x3f0 into register X ← COM1 port address


There are times when controllers need to read or write large amounts of data directly to or from system memory. For example when user data is being written to the hard disk. In this case, *Direct Memory Access (DMA)* controllers are used to allow hardware peripherals to directly access system memory but this access is under strict control and supervision of the CPU.