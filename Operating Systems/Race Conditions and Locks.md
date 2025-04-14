### Thread API (Mental Model)
- `thread_create(func, args)` - creates a new thread and passes the arguments in
- `thread_yield()` - thread voluntarily gives up the CPU
- `thread_join(tid)` - wait for other thread with ID `tid` to exit
- `thread_exit()` -exists
- Programs must work regardless of speed (when processor is working on that thread)
- Technically, kernel support to implement threads isn't required. However, there are huge benefits to having kernel support, such as the kernel scheduler being able to optimize expensive system calls and being aware of which threads are blocked

Reasoning about threaded code is **hard** - other threads might change memory or variables in between instructions in your program, which makes it hard to reason and build invariants. We have to **interleave** different instructions and see if it's correct. However, this only works on small programs, there are $2^n$ possible interleavings.

Instead, we can reason about **interference** - how much state can change from one instruction to the next? How much can another thread impact this one?

We start with **stable properties** - for example, "once `x` is at least one, it can never be below one" - which properties are monotonic, unchanging, etc.

### Sequential Consistency
A multithreaded program is equivalent to some interleaving of its threads. This is tricky because:
- We need to know what operations are atomic. `x += 1` is actually `t = x; x = t+1` 
- Compilers reorder instructions for performance, can only guarantee equivalence for single threaded
- Processors **also** reorder instructions - details vary by CPU and are complicated
- Write buffering
Unfortunately, no modern CPU/compiler/language guarantees Sequential Consistency for multithreaded operations. However, there is an agreed-upon standard that DRF $\to$ SC, which means that "data-race freedom implies sequential consistency."

A **race** condition is any situation where program behavior depends on thread schedule. 

### Good Solution: Locks!
- A lock is either busy or free
- A lock is initially free
- `acquire()` waits until lock is free, then atomically sets it to busy
- `release()` sets the lock to free