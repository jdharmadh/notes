.o files can't be executed by themselves. They're just compiled objects from source files.

The **ELF** (Executable and Linkable Format) consists of code and data segments, as well as descriptions of how to load the program into memory - can hold a complete program or part of a program. 


### More Than One Process
- For now, assume they are completely isolated in separate virtual address spaces
- Each might make its own syscalls, so we need one kernel stack per process
- Process Control Block (PCB) tracks state
- Questions:
	- *How to create new process?*
	- *How to switch between processes?*

### Creating a New Process
- Allocate and initialize PCB
- Create and initialize address space
- Load program, allocate user stack and heap
- Copy arguments into user stack (if invoked with arguments)
- Arrange trap frame to "resume" at preface
- Mark process as runnable

### Implementing Fork/Exec
- Fork: copy address space of parent
	- In child, arrange to return 0 for PID
	- In parent, arrange to return child PID
- Exec: load new program into address space
	- Arrange trap frame to resume at preface
- Can be sped up with copy-and-write 

### How to Switch Between Processes
Key idea: timer interrupt handler "resumes" to different process
- Keep a trap frame at the top of the kernel stack. During a timer interrupt, switch the stack pointer to the new kernel's kernel stack, it will pop off the appropriate user data and begin the new process!