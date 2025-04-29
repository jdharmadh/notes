### Scheduling Problem
- Input: a workload (set of tasks and arrival/completion times)
- Output - a schedule of when to run the CPU on what task

### Strategies
- FIFO: First job to arrive gets scheduled first (this usually fails as a greedy strategy)
- Shortest Job First: Prioritize shorter jobs, does much better for latency
	- Cannot be implemented because it requires advance knowledge of which jobs will arrive
- Round Robin: tries to approximate Shortest Job First
	- Each task gets CPU for fixed amount of time, then rotate through
	- How to pick the fixed amount of time - called the "quantum"?
		- Short quantum approximates Shortest Job First - but can do badly if jobs are pretty uniform and larger than the quantum
		- Long quantum approximates FIFO
### Fairness
Max-min fairness: Maximize the minimum allocation to any task. If any task needs less than their "faire share," just give them exactly what they need and divide the rest among other tasks.

### Multi-Level Feedback Queue
- Implements Round-Robin Scheduling at multiple levels
- Each level has its own quantum
- Scheduler moves tasks between levels depending on whether its runtime is dominated by CPU time or I/O