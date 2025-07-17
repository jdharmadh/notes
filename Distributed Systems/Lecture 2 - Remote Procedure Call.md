### Remote Procedure Call
- A request from a client to execute a function on a server
	- Client calls remote procedure
	- Client serializes parameters into a request message and sends it by TCP/UDP/etc
	- Server receives request, parses it, calls local procedure, and sends a reply message
	- Client receives reply and continues execution
- RPC requires an interface description language (IDL)
	- Generates ser/des code automatically and stubs for client/server
- RPC needs binding (connection between client and server)
	- Network connection, make sure server has required function, etc
### Naive RPC
- Any numbers of clients and servers with no state
- Client sends a message, server executes and sends a reply
- Client doesn't know if message was received and executed if sever doesn't reply!
### Improving on Naive RPC
- Create a client timer that retransmits message if reply not received within certain time
- Give each request a unique ID to avoid duplicate messages leading to duplicate operations
### Types of RPC
- At least once: 
	- Client resends on timeout, execute every copy that arrives at the server
	- If client gets a reply, executed **at least once**
	- If no reply, may have been executed, maybe multiple times
- At most once:
	- Execute only the first copy of the request, every message after just retransmit the result
	- If client gets a reply, executed **at most once**
	- If no reply, may have been executed one or zero times
### Garbage Collection: When can Server Discard Old Replies