An upcall can be thought of as a reverse system call. Upcalls allow the kernel to deliver an asynchronous notification to a process, even if the process did not execute any system call.
Upcalls are used for:
- Asynchronous I/O notification
	- Syscall to enqueue operation, signal to notify that it is complete
- User-level exception handling
	- e.g. Microsoft Word autosaves unsaved files before crashing
- User-level thread libraries can deliver hardware timer fires

### Virtual Machines
Consists of a host kernel, which interacts with the hardware, and a guest kernel, which is running on the host kernel. 

Why do we need virtual machines?
- Isolate application environments
- Efficient use of server hardware
- Transparent hardware upgrade
	- Save entire state of VM and resume
- OS development

Can we have a VM inside a VM inside a vm? **Yes!** But it's not supported because the performance degrades horribly. One layer is usually enough. 

How to run a system call / hardware interrupt?
- When the guest kernel attempts a privileged instruction, the CPU invokes a permission denied exception handler - which we have specifically configured in the host OS to emulate the system call