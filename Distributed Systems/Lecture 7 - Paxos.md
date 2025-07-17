### Problems to Address
- View Server can Fail
- For vector clocks, we need acks from all the other servers before we respond to the client

### What is Paxos?
- Paxos is a family of distributed consensus algorithms 
- **Consensus**: Group of processes decide on one and only one value
- **Availability**: System can make progress as long as s majority of the processes are alive
- Use cases:
	- Replicate some application state (labs)
	- Maintain cluster configuration information (what the view server does in primary-backup)
### Original Paper: FLP
- **Theoretical result**: Impossible for a deterministic protocol to guarantee consensus in bounded time in an asynchronous distributed system (even if no failures actually occur and all messages are delivered)
- Paxos: always safe, non-blocking as long as a majority of participants are alive and messages are eventually delivered
- Key idea that majorities intersect: for any two majorities S and S', there is some node in both S and S'
### State Machines Replication
- Goal: nodes agree on order of operations, despite failures and asynchrony
- Think of sequence of operations as a log, once item's place in the log is decided, it **never changes**
- Problem: client requests can reach servers in different order

### Consensus
- Consensus is easy if there is a leader:
	- All clients send requests to leader, leader picks which operations goes first, **proposes** to everyone else
- Problem: What if leader failed or is slow?
	- If leader failed, we need a new leader
	- If leader is slow and we pick a new leader, we might have two leaders
- Each leader makes a proposal for the next slot
	- We could end up with multiple simultaneous proposals for one slot, we need to make sure only one is actually chosen 

### Basic Model for the Protocol
- A set of processes that can propose values
- Processes can crash and recover, have access to stable storage (labs don't test this)
- Asynchronous and unreliable network
- Deciding just one slot at a time is called "Paxos"
- Deciding multiple slots at a time is called "Multipaxos"

### Paxos Terminology
- **Value**: a possible operation to put in the next slot in the operation log
- **Proposal**: Tuple\[Integer, Value\]. A request to select a value; proposals have unique numbers
	- Same as ballot in Multipaxos
- **Accept**: a yes vote on a specific proposal
- **Chosen**: Same proposal accepted by a majority of acceptors
	- "Chosen" is not the same thing as "voted"
- **Learned**: Fact that proposal was chosen is known
### Roles for Servers
- **Proposers**: N, like a *leader* or *primary*
- **Acceptors:** vote yes or no on proposals
- **Learners:** application replicas. Execute on chosen decisions
- In the labs, and in practical systems, each server plays all three roles
### Phases
- **Prepare phase:** Proposer contacts acceptors to decide what proposal to put up for vote. Called "p1" in Multipaxos.
- **Accept phase:** Proposer sends its proposal to acceptors to vote Majority accepts $\to$ value is chosen. Called "p2" in Multipaxos.
- **Learn phase:** Learners discover the chosen proposal

### Prepare Request
1. Send *prepare* request to all acceptors with proposal number p
2. Acceptor promises not to accept any proposal
3. Acceptor replies with highest proposal they've accepted

### Accept Request
1. Send *accept* request to all acceptors, with value of highest proposal among *prepare* replies
2. Acceptor accepts if they can, according to past promises
3. Value chosen if a majority of **all** acceptors accepts