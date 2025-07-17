### Primary Backup
- **When execution is happening normally:** replicate application state on two servers
- **When one application crashes**: reroute all requests to the replica
### View Server
- Designate a server as the primary, and other servers as backup
- When client wants to do an operation, asks a special server called the "view server" which server is the primary
- View Server responds with which server is the primary, and the client sends operations to that server
- The primary then sends messages to the backup servers to make sure their states are aligned
### State Machine Replication
- Think of server as a state machine, and each client as sending operations
- Backups are copies of the state machine, and we just need to make sure we execute operations in the same order on primary and backup
- Guarantees consistency:
	- Each operation is deterministic
	- Each copy executes the same sequence of operations
	- Implies: operations execute one at a time
### Two Approaches to Primary Backup in State Machine Replication
- When primary receives some operations, send them to the backup with a sequence number, and then the backup will execute when it gets them
- (RECOMMENDED) do them together - primary receives operation, sends to backup, waits for backup reply, then executes operation and responds
### More on the Second Strategy
- If there are no failures, we should keep primary and backup invariant (see rule 1)
- If there are failures, it should be clear who the new primary and backups are (rule 2)
- How does the view server detect failures
	- Every node keeps pinging the view server
	- A node is considered "dead" if it has missed *n* pings
	- If we detect a failure, we need to create a view change (new primary and backup)
		- New primary sends its state to new backup
		- Backup initializes new state, acks to primary
		- After receiving ack, primary pings to view server
		- View server starts telling clients to use the new view
# Rules:
1. Primary must wait for backup to execute and reply each operation before executing operation itself and responding to client.
2. Primary in view i+1 must have been backup or primary in view i.
(See [[Lecture 4 - More Primary Backup]]) for the next rules
3. Backup must accept forwarded requests only if view is correct.
4. Every operation must be before or after state transfer.
5. Non-primary must reject client requests.
6. View server cannot change views until current primary has acked the view.