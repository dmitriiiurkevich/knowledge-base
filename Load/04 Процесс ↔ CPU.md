Process 1:

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

```assembly
01000000 00001100
01000001 00010100
00000000 00000001
10000000 10001111
...
```

machine code → process 1 address space

```memory
01000000 00001100 → 1003
01000001 00010100 → 1004
00000000 00000001 → 1005
10000000 10001111 → 1006
...
```

Process 2:

```js
fn main() {
	let a = 100 + 35;
	//..
}
```

JavaScript → assembly

```assembly 
LOAD R0 100
LOAD R1 35
ADD R0 R1
STORE R0 addr_a
...
```

assembly → machine code

```machine
01000000 01100100
01000001 00100011
00000000 00000001
10000000 10001111
...
```

machine code → process 2 address space

```memory
01000000 01100100 → 863456
01000001 00100011 → 863457
00000000 00000001 → 863458
10000000 10001111 → 863459
...
```

Processor's states:

```processor
Reg 0 = 0 ←←← from memory [active process context]
Reg 1 = 0 ←←← from memory [active process context]
Reg 2 = 0 ←←← from memory [active process context]
Reg 3 = 0 ←←← from memory [active process context]
Instruction reg = 0 ←←← from memory [active process context]
Address reg = 1003 ←←← from memory [active process context]
```
   $\downarrow$ 
```processor   
Reg 0 = 0
Reg 1 = 0
Reg 2 = 0
Reg 3 = 0
Instruction reg = LOAD R0 12 ←←← from memory 1003
Address reg = 1003
```
   $\downarrow$
```processor
Reg 0 = 12 ←←← to register
Reg 1 = 0
Reg 2 = 0
Reg 3 = 0
Instruction reg = LOAD R0 12
Address reg = 1003
```
   $\downarrow$
```processor
Reg 0 = 12
Reg 1 = 0
Reg 2 = 0
Reg 3 = 0
Instruction reg = LOAD R0 12
Address reg = 1004 ←←← +1
```
   $\downarrow$
```processor
Reg 0 = 12
Reg 1 = 0
Reg 2 = 0
Reg 3 = 0
Instruction reg = LOAD R1 20 ←←← from memory 1004
Address reg = 1004
```
   $\downarrow$
```processor
Reg 0 = 12
Reg 1 = 20 ←←← to register
Reg 2 = 0
Reg 3 = 0
Instruction reg = LOAD R1 20
Address reg = 1004
```
   $\downarrow$
```processor
Reg 0 = 12
Reg 1 = 20
Reg 2 = 0
Reg 3 = 0
Instruction reg = LOAD R1 20
Address reg = 1005 ←←← +1
```
   $\downarrow$
```processor
Reg 0 = 12
Reg 1 = 20
Reg 2 = 0
Reg 3 = 0
Instruction reg = ADD R0 R1 ←←← from memory 1005
Address reg = 1005
```
   $\downarrow$
```processor
Reg 0 = 32 ←←← add
Reg 1 = 20
Reg 2 = 0
Reg 3 = 0
Instruction reg = ADD R0 R1
Address reg = 1005
```
   $\downarrow$
```processor
Reg 0 = 32
Reg 1 = 20
Reg 2 = 0
Reg 3 = 0
Instruction reg = ADD R0 R1
Address reg = 1006 ←←← +1
```
   $\downarrow$
```processor
Reg 0 = 32
Reg 1 = 20
Reg 2 = 0
Reg 3 = 0
Instruction reg = STORE R0 addr_a ←←← from memory 1006
Address reg = 1006
```
   $\downarrow$
```processor
Reg 0 = 32 →→→ to memory addr_a
Reg 1 = 20
Reg 2 = 0
Reg 3 = 0
Instruction reg = STORE R0 addr_a
Address reg = 1006
```
   $\downarrow$
```processor
Reg 0 = 32
Reg 1 = 20
Reg 2 = 0
Reg 3 = 0
Instruction reg = STORE R0 addr_a
Address reg = 1007  ←←← +1
```
   $\downarrow$
   $\vdots$
   $\downarrow$
```processor
Reg 0 = 32 →→→ to memory [current process context] 
Reg 1 = 20 →→→ to memory [current process context]
Reg 2 = 0 →→→ to memory [current process context]
Reg 3 = 0 →→→ to memory [current process context]
Instruction reg = STORE R0 addr_a →→→ to memory [current process context]
Address reg = 1007 →→→ to memory [current process context]
```
   $\downarrow$
```processor
Reg 0 = 0 ←←← from memory [active process context]
Reg 1 = 0 ←←← from memory [active process context]
Reg 2 = 0 ←←← from memory [active process context]
Reg 3 = 0 ←←← from memory [active process context]
Instruction reg = 0 ←←← from memory [active process context]
Address reg = 863456 ←←← from memory [active process context]
```
   $\downarrow$
   $\vdots$

