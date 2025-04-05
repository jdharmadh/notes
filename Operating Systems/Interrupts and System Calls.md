### What must be true about kernel mode transfer?
- Kernel must control entry points (app can't jump to arbitrary kernel code)
- Program counter, stack pointer, privilege level must change
	- Can't use process' stack, it could be invalid or point to random memory
- Old values of ^ must be saved 
	- "Transparently" restart the process
	- Mode transfers must happen at known instruction stream
### Privilege Levels
- x86 has 4 privilege levels
- "Level 0" is kernel mode
- "Level 3" is user mode
- The Current Privilege Level (CPL) is stored by x86 in the FLAGS register

### Interrupts
- "Interrupt vector" where each interrupt is assigned a number
	- 0 is division by zero
	- 6 is a bad instruction
- There is a special hardware register (called IDTR on x86) that will signal when there is a hardware interrupt
- Transfer control to kernel to handle
- All of the current process state is stored in a data structure called a "trap frame"
- x86 uses an instruction called `iret` to restore all the process state
- System calls are basically software interrupts that are handled like this