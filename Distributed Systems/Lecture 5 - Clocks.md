### Why do we need clocks?
- Correctness property of our system: **consistent ordering**
	- Everyone agrees on the same ordering
	- Ordering respects causality: If A causes B, then A should happen before B
	- Or: ordering respects real-time (which implies the causality)
- The way we define time can tell us which of two concurrent events happened first
### Two Approaches to Clocks
Physical Clocks
- Every computer has an (inaccurate) clock
- Maybe we can fix those inaccuracies?
Virtual Clocks
- Respects causality, despite arbitrary message or computation delays
- No relationship to physical time
### Physical Time
- Server clocks drift relative to real-time
	- Rate of drift depends from machine to machine, and also  on temperature
- Fix: Network Time Protocol
	- Clients query time servers
	- Time = server's clock - 1/2 * round trip time
	- Average over several time servers, throw out outliers
	- In between queries, adjust for measured clock skew
	- Huygens system at Google can do this to improve the error to < 100 nanoseconds
### Virtual Clocks
A way to order events with no assumptions about physical clock skew, message delays, or computation time, using only local information, with globally valid timestamps (everyone agrees on the order), that respects causality.

Happens-before semantics:
- A should happen before B if:
	- A happens earlier than B at the same location
	- A is the send and B is the receipt of a message
	- Transitive: If A is before C and C is before B
#### Logical Clock Implementation
- Keep a local clock $T$
- Increment $T$ whenever an event happens
- Send clock values on all messages $T_m$
- On message receipt: $T = \max (T, T_m) + 1$

#### Lamport Clocks have goals in this model
- If A happens before B, $T(A) < T(B)$
- Contrapositive: if $T(B) \geq T(A)$, A does not necessarily happen before B
- Next lecture we will define a system where the other direction holds:
	- If $T(A) < T(B)$, A happens before B