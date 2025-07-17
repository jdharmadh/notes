### Intro
- Represent transitive causal relationships
- $T(A) < T(B) \iff$ A happens before B
- Track events known to each node, *on each node*
### How it works
- Clock is a vector C, length is number of nodes
- On node $i$, increment $C[i]$ after each event
- On receipt of message with clock $C_m$ on node $i$
	- Increment $C[i]$
	- for each $j \neq i$
		- $C[j] = \max (C[j], C_m [j])$
- Merge local logs after the fact
	- Put x before y if $C_x$ happens before $C_y$ 
	- Put y before x if $C_y$ happens before $C_x$
	- 