## Query Execution
- Parser: parses query into an internal format, then performs various checks using the Catalog
- Optimizer: Find an efficient query plan for executing the query
	- Logical plan: Relational algebra tree that matches the query
	- Physical plan: Additional annotations on the nodes that describe how to access the data
- Executor: runs the physical plan
- Push-vs-pull execution:
	- Pull: Executor requests tuples when it wants to process a tuple
	- Push: Push tuples to executor for processing
	- Most modern distributed systems use push-based interfaces because less network calls are required
### Storage Manager
How do we efficiently manage data in a database?
- Access methods: organize data to support fast access of subsets of records
- Buffer Manager: cache data in memory
- Disk Manager: I/O with disk