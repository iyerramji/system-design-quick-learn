### FUNCTIONAL REQUIREMENTS
  - Demonstrate technical leadership by discussing the architecture and not seeking guidance. If you feel that input from the interviewer is helpful, avoid a direct question, such as "What do you think I can focus on next?". Instead, structure the question as "OK, next we can focus on A, B or C. Do you have preference?"
  - Budget the time to ensure discussing the topics that were agreed with the interviewer earlier. As a rule of thumb, cover those topics at a high level first and then have deeper discussion as the time allows.


### NON-FUNCTIONAL REQUIREMENTS
Repo to quickly revise system design



### BACK OF ENVELOPE
Repo to quickly revise system design


### HIGH LEVEL DESIGN
  - Service architecture.



### DETAILED DESIGN FOR SINGLE DATACENTER
  - continue doing tradeoffs during the session
  - make sure to write down schemas for tables, caches, etc
  - lead the discussion yourself
  - discuss trade offs for decisions/etc you make
  - Justify DB selection for the data - SQL, NoSQL (key-value, document, graph). For example, consider if we need ACID property (SQL have stronger support of ACID), how much data will be stored, how quickly it will be growing and if the types of queries will change over time.
  - completeness of the solution and trade-offs as that is what I would expect from an E5
  - Always do an end to end run
  - discuss the read/write/update path
  Trade-offs: discuss the positives and negatives of the design that was proposed
  - You could have talked about why we need high availability
  - You need to cover more trade-offs
  - SQL vs NoSQL


### SCALE IT / MULTIPLE DATA CENTERS
  - metrics/thinking about how system can break and how to watch for it is a good thing to discuss
  - edge cases, points of failure, etc.
  - Points of failure, edge cases.
  - Schema design to address the usage pattern, including indexing, sharding.
  - DB sharding, replication and synchronization
  - Scalability (LBs, Cache, CDNs, DNS, etc).
  - sharding vs partitioning, noSQL vs SQL, push vs pull, how to do pagination, different caching policies, etc
  -  Caching
  - Load Balancing
  - Partitioning
  - sharding
  - talk about bottlenecks


### BILL OF MATERIALS ( OPTIONAL)
  - Hardware requirements estimation.
