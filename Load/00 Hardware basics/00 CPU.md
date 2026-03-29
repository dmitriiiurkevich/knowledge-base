CPU

The processor's execution is governed by the *system timer*. 

The *system timer* generates regular clock pulses to the processor. → Each clock pulse, the processor execute one of *instructions*, like:
- read the contents of memory at location X into register Y
- write the contents of register X into memory at location Y
- write into register X sum of contents of registers X and Y
- ...

JavaScript program

```js
fn main() {
	let a = 12 + 20;
	//...
}
```

JavaScript → assembly

```assembly
LOAD R0 12
LOAD R1 20
ADD R0 R1
STORE R0 addr_a
...
```

assembly → machine code

```machine
01000000 00001100
01000001 00010100
00000000 00000001
10000000 10001111
...
```

*Registers* are the microprocessor's internal storage.

The size, number and type of *register* within a microprocessor is entirely dependent on its type. But most processors have the following special purpose, dedicated, *registers*:
- *Program Counter (PC)* — points to the instruction
- *Stack Pointer (SP)* + *Extended Base Pointer (EBP)* — points to the data
- *Processor Status (PS)* — defines the processor current mode: *kernel mode* or *user mode*.

*Program Counter (PC)* — contains the memory address of the next instruction to be executed. 

The contents of the PC are automatically incremented each time an instruction is fetched. But the operations performed may cause the processor to stop what it is doing and jump to another instruction somewhere else in memory. 

*Stack Pointer (SP)*  — contains the memory address of the last data element added to the *stack*.

In most cases, when a function call is made within a program, a *stack frame* is created on the stack to support that function's data. The *stack frame* provides a logical structure for storing the function's parameters, local variables and other related data.

Each function generates its own *stack frame*, regardless of the function hierarchy within the program. 

Each *stack frame* contains
- the target function local variables,
- *return address* — a memory address of the *instruction* where program to return after the *target function* exits,
- some additional parameters.

Another processor register — *Extended Base Pointer (EBP)* — is used for navigation within the *stack frame*.


![[Screenshot 2025-04-05 204059.png|450]]




