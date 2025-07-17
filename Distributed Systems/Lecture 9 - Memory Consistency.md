### Consistency
The allowed semantics of a set of operations to a data store or shared object.
- Represents what the system is **allowed** to do
- Contract between program and system, not tied to implementation
- Terminology:
	- **Strong consistency**: the system behaves as if there's just a single server
	- **Weak consistency**: many possible models, that allow some violation of single store model
	- **Eventual consistency**: weak consistency, but any anomalies are temporary
### Linearizability
- Behaving as if there's a single correct, copy
- Behavior on a set of client requests is equivalent to **some** sequential history, i.e. a total ordering
- Respects real-time ordering
	- If A ends before B starts, A should happen before B in the sequential history
### Sequential Consistency
- Behavior on set of client requests is equivalent to some sequential history that respects the local ordering at each node
	- Still a single total order, but the order does not need to respect real time
- In databases, when applied to transactions:
	- Strict serializability = linearizability
	- Serializability =sequential consistency 