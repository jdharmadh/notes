Allows us to describe the performance of any system by modeling their behavior in an abstract queueing model.

### The Model
- Requests get put into a server's queue, they are processed, then a response is sent
- Example: Server processes 1 request at a time, takes 1ms to process a request. We could say that the server can process 1000 requests per second, but **that's not the whole story!**
	- If requests arrive exactly every 10ms, the throughput is 100 requests / second and the latency is at most 1 ms
	- If requests arrive exactly every 2ms, same thing since the number is still higher than the server's processing time
	- Let's say requests are arriving exactly 1ms - maximum server utilization. If **one** extra request comes in, it will grow the queue of waiting requests by 1
	- What about 0.99 ms? The latency will get arbitrarily worse - this is called **overload**, running a system past its capacity