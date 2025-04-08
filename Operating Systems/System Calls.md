To execute a system call, we use a **software interrupt:**
- Software interrupt (in contrast to hardware interrupts) is called using the `int` instruction on x86, which takes the interrupt code as an argument and invokes the appropriate handler
- All system calls are assigned the same interrupt code, but they are also called with a separate **system call number** which identifies which system call to execute

#### Pair-of-Stubs Approach
- User space function that the user can call ("user stub")
- User stub calls interrupt, which invokes a handler: the handler does some checks, copies the arguments into the kernel, and calls the function that actually does the work - "kernel stub"
- Allows separation between the user call and the true executing function via a stub on each side

### Securing System Calls
System calls are **inherently dangerous**.
- Kernel has permission to do anything, so we must manually check that the user's programs has proper permissions
- TOCTTOU error - "Time of Check to Time of Use error" - if we check the arguments before checking permissions, the memory corresponding to the arguments might change between us checking them and us using them. This is why we have to **copy the arguments**! 