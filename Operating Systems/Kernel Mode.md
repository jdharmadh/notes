
### An Old (But Useful) Model - Running Programs in 1981
When a program runs:
- Instructions are copied from a `.out` file into memory
- Allocate an empty heap and stack
- Set the stack pointer appropriately
- Jump to `main()` 
When running multiple copies of the same program, each copy needs:
- Its own stack
- Its own copy of any mutable data
- All of the global data + heap
- Could possibly share code
#### Process
- A process is an _instance_ of a program
- Each instance has its own copy of the program in memory
- In the basic model, assume each process is single threaded

What happens if programs running on a computer are malicious or have a bug? In 1981, bad things! But today, we want a better model.

### Today's Process
- A process is an instance of a program that **runs in a sandbox**
- A process can only access its own memory
- Cannot perform "dangerous" IO
- Cannot hog resources

#### Idea 1: Simulate the CPU
- Instead of executing on hardware, simulate the CPU
- Can check for infinite loops, out-of-bounds memory accesses, etc.
- Unfortunately, **massively** slower

#### Idea 2: Implement Checks in Hardware
- We keep dual-mode operations, CPU has an extra bit which keeps track of mode
- In **user mode**, CPU checks each instruction before executing
  In **kernel mode**, no checks

### What to Check?
- Prevent program from executing privileged instructions
	- An instruction is **privileged** if it can only be executed in kernel mode
	- Instructions that change the mode (except for system calls!)
	- Instructions that configure what memory the app can access
	- Instructions that configure interrupt handling
	- If an app tries a privileged instruction:
		- Idea 1: Treat it as no-op. Safe, but frustrating to debug for program developer
		- Idea 2: Raise a processor exception (transfers control to exception handler in kernel)
- Memory protection
	- Idea 1: Assign each process a contiguous range of addresses it can access, hardware simply checks that program is allowed to access that memory
	- Idea 2: Virtual Memory. Give each process a full address space, but on hardware kernel is managing where the addresses actually map to
		- Configuring the mapping of virtual memory $\to$ physical memory is a privileged instruction!
- Timer interrupts
	- OS must be able to "take back" the CPU in case of infinite loop or Ctrl-C interrupt
	- Configure a hardware timer to interrupt, which transfers control back to OS, switches to kernel mode, and calls the kernel's interrupt handler