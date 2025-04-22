Deadlock is when multiple threads are stalled because they are waiting for each other. 

### Necessary Conditions
There are a few necessary conditions for deadlock:
- Bounded resources
	- If there are unbounded resources for threads to use, there cannot be deadlock as each thread will get its necessary resources. However, this is not always possible. 
- No resource preemption
	- Once a thread starts holding a resource, only it can release it. One way to prevent deadlock is to allow some central controller to forcibly reclaim resources from threads.
- Wait while holding
	- We can eliminate deadlock by disallowing threads to hold a resource while they are waiting for another resource.
- Circular waiting
	- When there is a cycle in who is waiting for resources. We can try to stop this by acquiring resources in some global order.
	- Idea: Assign some order to locks/resources, then only acquire locks in that order.

### Eliminating Deadlock
- Avoidance
	- Write the program such that one or more of the necessary conditions is false
- Prediction
	- Wait until all future resources are available then atomically acquire all of them
	- Acquire-all / Release-all strategy 
		- Programs declare all the resources they need up front, and then those requests are delated until those resources are free
	- Banker's Algorithm
		- Grant requests as long as there is some sequence of thread executions that allows each grant request to receive its max resources
- Detection
	- Undo changes/operations that caused deadlock
	- Transactions 👀