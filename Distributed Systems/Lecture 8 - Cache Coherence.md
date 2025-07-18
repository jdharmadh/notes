- Want to use caches to take advantage of spatial/temporal locality
- Idea: when performing a write, ensure there is only one copy
	- When performing reads, allow multiple copies
- Idea: Leases
	- Lease - a time-limited right to do something 
		- Can be renewed
		- Unlike Paxos, depends on loosely synchronized clocks
	- Lease fault tolerance:
		- If lease holder or network fails: wait for lease to expire
		- Plus epsilon to account for clock drift
		- Hand lease to someone new
		- A lease is like a distributed lock, but fault-tolerant