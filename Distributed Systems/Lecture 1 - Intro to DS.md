### Distributed Systems
- A group of computers that have no shared state (must communicate with each other, and communications can fail)
### Model
- Failure Model (Fault Model)
- Asynchronous fail stop computers
	- **Asynchronous**: computer might be slow to respond while still working correctly
	- **Failure by crashing**: computer fails by stopping - it never sends a wrong answer or violates the protocol
- Network is asynchronous and may delay, drop, reorder, or duplicate messages
	- It might delay messages while still working correctly
### Simplifications made for the Class
- Network will not corrupt messages
- Network is commutative and transitive
	- If A can talk to B, B can talk to A
	- If A can talk to B and B to C, then A can talk to C
- Clients only make one request at a time
- Simulate server failures by partitioning (network cuts some servers off from each other)
### Considerations in the Fault Model
- Can the computer tell if there is a problem?
	- Was the message I sent delivered, or is the network slow?
	- Has the other computer crashed, or is it slow? Or is the network slow?
### What do We Value in a Distributed System?
- Reliable
	- Available (high uptime)
- Efficient
- Low Latency
- Huge scale and scalable