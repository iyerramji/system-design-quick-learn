### FUNCTIONAL REQUIREMENTS
who is the end user ?
spiky or continuous traffic ?
Authentication etc ?
Metric or logging etc ? know 4 golden signals => latency, error_rate, saturation,

Daily Active User ?
READ/WRITE ratio ?
- How do we expect this to grow over time?"





### NON FUNCTIONAL REQUIREMENTS
- DURABLE STORAGE
- EVENTUALLY CONSISTENT ?
- HIGHLY AVAILABLE ?
- LOW LATENCY


### BACK OF ENVELOPE CALCULATIONS
- data growth
- throughput/traffic incoming data in terms of MBPS or GBPS for each API.
- latency of each API
- traffic interms of qps


### HIGH LEVEL DIAGRAM





### DETAILED DIAGRAM / SINGLE DC
- API DESIGN
- DB SCHEMA ( with tradeoff)
- END TO END FLOW
- TRADEOFFS.




### SCALE IT / MULTIPLE DC
- LB types
- CAche types
- partitioning/replication/sharding
- bottlenecks
- edge cases
- point of failure
- cap theorem




### BILL OF MATERIALS
