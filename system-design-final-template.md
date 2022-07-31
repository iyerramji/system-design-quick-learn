### FUNCTIONAL REQUIREMENTS
who is the end user ?
spiky or continuous traffic ?
Authentication etc ?
Metric or logging or Telemetry etc ? know 4 golden signals => latency, error_rate, saturation, traffic

Daily Active User ?
READ/WRITE ratio ?
- How do we expect this to grow over time?"
What scale is expected from the system (e.g., number of new tweets, number of tweet views, number of timeline generations per sec., etc.)?





### NON FUNCTIONAL REQUIREMENTS
- DURABLE STORAGE
- EVENTUALLY CONSISTENT ?
- HIGHLY AVAILABLE ?
- LOW LATENCY
- The system should be highly reliable; any uploaded photo or video should never be lost.


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
- Single point of failure ( Is there any single point of failure in our system? What are we doing to mitigate it?)
- cap theorem
Identifying bottleneck examples =>
  Do we have enough replicas of the data so that we can still serve our users if we lose a few servers?
  Similarly, do we have enough copies of different services running such that a few failures will not cause a total system shutdown?
  How are we monitoring the performance of our service? Do we get alerts whenever critical components fail or their performance degrades?




### BILL OF MATERIALS
