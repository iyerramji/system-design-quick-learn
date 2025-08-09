#### Bloom filter

#### quorum

#### sloppy quorum


#### Vector clocks

#### Read Repair

#### Geofencing

#### Merkle trees

#### HeartBeat

#### Gossip Protocol


#### High water mark


#### CAP theorem


#### Split BRain


#### Write ahead logging

#### Segmented logging


#### LEader adn follower

#### Consistent Hashing


#### Hinted handoff




Here’s the **SRE-friendly breakdown** of common **load balancing algorithms**, with examples of where they’re used in real systems.

---

## **1️⃣ Round Robin**

* **How it works:** Sends each new request to the next backend in sequence, looping around.
* **Use case:** Simple, even distribution when all servers have similar capacity.
* **Example:** NGINX default LB method for HTTP.
* **Pros:** Easy to implement, predictable.
* **Cons:** Ignores server load; can overload slow nodes.

---

## **2️⃣ Weighted Round Robin**

* **How it works:** Like Round Robin, but servers have weights; higher weight gets more requests.
* **Use case:** Mix of big and small servers.
* **Example:** F5 BIG-IP, NGINX `weight` parameter.
* **Pros:** Handles heterogeneous capacity.
* **Cons:** Weights must be tuned manually.

---

## **3️⃣ Least Connections**

* **How it works:** Sends new requests to the server with the fewest active connections.
* **Use case:** Good for long-lived or unevenly sized requests.
* **Example:** HAProxy `leastconn` algorithm.
* **Pros:** Adapts to current load.
* **Cons:** Needs accurate connection tracking; may not suit stateless short requests.

---

## **4️⃣ Weighted Least Connections**

* **How it works:** Combines server capacity weight with least-connections choice.
* **Use case:** Mix of high-capacity and low-capacity nodes with varying active load.
* **Example:** HAProxy, AWS ALB target group settings.
* **Pros:** Balances both capacity and load.
* **Cons:** Slightly more complex to tune.

---

## **5️⃣ Least Response Time**

* **How it works:** Sends to the server with the lowest average response time (and/or fewest active connections).
* **Use case:** Web APIs with variable backend performance.
* **Example:** NGINX Plus, Envoy advanced LB.
* **Pros:** Reacts to slow servers.
* **Cons:** Needs good health/latency metrics.

---

## **6️⃣ IP Hash / Source Hash**

* **How it works:** Hash client IP → pick a backend based on hash result.
* **Use case:** Simple session persistence (“stickiness”) without cookies.
* **Example:** NGINX `ip_hash`, Envoy `hash_policy`.
* **Pros:** Sticky sessions without extra state.
* **Cons:** Poor balance if clients are unevenly distributed; breaks if client IP changes (NAT).

---

## **7️⃣ URL Hash / Header Hash**

* **How it works:** Hash based on request URL, header, or cookie.
* **Use case:** Cache servers; same content request → same server.
* **Example:** CDN edge caches.
* **Pros:** Good cache hit rate.
* **Cons:** Doesn’t adapt to server load.

---

## **8️⃣ Random with Two Choices**

* **How it works:** Pick two random backends → choose the one with fewer active connections.
* **Use case:** High-scale systems; better than pure random.
* **Example:** Some cloud LBs, internal service mesh implementations.
* **Pros:** Simple, avoids worst-case imbalance.
* **Cons:** Still not as precise as least-connections.

---

## **9️⃣ Consistent Hashing**

* **How it works:** Hash key (IP, user ID, etc.) → map to backend on a ring. Only remaps a small portion of keys when nodes change.
* **Use case:** Distributed caches (Memcached, Cassandra).
* **Example:** Envoy `ring_hash`, Maglev in GCP LBs.
* **Pros:** Stable routing, minimizes cache misses when scaling.
* **Cons:** More complex; doesn’t balance perfectly.

---

## **🔟 Geolocation-based**

* **How it works:** Route client to nearest (or regionally assigned) server.
* **Use case:** Global CDNs, multi-region apps.
* **Example:** Cloudflare, AWS Route 53 geolocation routing.
* **Pros:** Low latency for users.
* **Cons:** Can cause uneven load; location detection may be wrong.

---

## **1️⃣1️⃣ Performance/Cost Aware**

* **How it works:** Route based on backend metrics (CPU, memory, cost) or cloud pricing.
* **Use case:** Cost optimization or workload-aware routing.
* **Example:** Custom service mesh policies, GKE multi-cluster ingress with load awareness.
* **Pros:** Smart resource use.
* **Cons:** Needs accurate telemetry; more complex.

---

💡 **Interview Tip:**
If they ask *“Which LB algorithm would you pick?”*:

* First: clarify **traffic pattern** (short-lived? long-lived? even or bursty? needs stickiness?).
* Then: choose algo that balances **fairness vs cost vs complexity**.
* Always mention **health checks** — no LB algo works well if you send traffic to broken backends.

---

If you want, I can also make a **decision matrix**: traffic pattern × LB algorithm × pros/cons — that’s the cheat sheet SREs use when designing real LB setups in Kubernetes or cloud.
Want me to build that?


#### Read Repair

#### Checksum



Got it — here’s a **clear breakdown of NoSQL database types** with **real-world examples** and **how they’re actually used** in SRE/infrastructure contexts.

---

## **1️⃣ Key-Value Stores**

* **What they are:**
  Simplest form of NoSQL — store data as a dictionary/map where a **key** points to a **value** (opaque blob).
* **Best for:**
  Ultra-fast lookups, caching, session storage.
* **Examples:**

  * **Redis** – in-memory, supports TTL, pub/sub, Lua scripts.
  * **Amazon DynamoDB** – fully managed, highly available, persistent key-value store.
  * **Riak KV** – distributed, fault-tolerant.

**SRE use case:**

* Store user session tokens in Redis for sub-millisecond retrieval.
* Cache ML inference results to reduce GPU usage.

---

## **2️⃣ Document Stores**

* **What they are:**
  Store semi-structured data as JSON/BSON/XML documents.
  Flexible schema — each document can have different fields.
* **Best for:**
  Applications needing flexible schema + rich querying on document fields.
* **Examples:**

  * **MongoDB** – most popular document DB, supports indexes, aggregation pipelines.
  * **Couchbase** – key-value + document store hybrid.
  * **Amazon DocumentDB** – MongoDB-compatible managed service.

**SRE use case:**

* Store config for microservices as JSON documents.
* Save chatbot conversation logs with flexible structure.

---

## **3️⃣ Column-Family Stores**

* **What they are:**
  Store data in **columns grouped into column families**, optimized for analytical queries and wide tables.
* **Best for:**
  High write throughput, time-series data, analytics on large datasets.
* **Examples:**

  * **Apache Cassandra** – highly available, horizontally scalable.
  * **HBase** – built on Hadoop/HDFS.
  * **ScyllaDB** – Cassandra-compatible, written in C++ for speed.

**SRE use case:**

* Store metrics (timestamp, metric name, value) for billions of rows — e.g., Prometheus long-term storage in Cassandra.
* Time-series event logs from IoT devices.

---

## **4️⃣ Graph Databases**

* **What they are:**
  Store data as **nodes** (entities) and **edges** (relationships) with properties.
  Optimized for traversals and relationship-heavy queries.
* **Best for:**
  Social networks, fraud detection, recommendation engines.
* **Examples:**

  * **Neo4j** – most popular graph DB with Cypher query language.
  * **Amazon Neptune** – supports Gremlin and SPARQL.
  * **ArangoDB** – multi-model (graph + document).

**SRE use case:**

* Map microservice dependencies to trace fault impact.
* Detect security anomalies by analyzing network connection graphs.

---

## **5️⃣ Time-Series Databases** *(specialized category)*

* **What they are:**
  Optimized for time-stamped data with efficient compression and queries over time ranges.
* **Best for:**
  Metrics, observability, IoT sensor data.
* **Examples:**

  * **InfluxDB**, **TimescaleDB** (PostgreSQL extension), **VictoriaMetrics**.
* **SRE use case:**
  Store and query infrastructure metrics (CPU, memory, GPU utilization) for dashboards and alerts.

---

## **6️⃣ Multi-Model Databases**

* **What they are:**
  Support multiple NoSQL data models (document + key-value + graph) under one engine.
* **Best for:**
  Complex applications needing different query styles.
* **Examples:**

  * **ArangoDB** – graph, document, key-value.
  * **Couchbase** – key-value + document.
  * **OrientDB** – graph + document.

**SRE use case:**

* Run both service dependency graph queries and JSON config lookups in one database.

---

## **📌 Interview Tip**

If they ask *“What type of NoSQL DB would you choose?”*, answer:

> “It depends on the access pattern and data model — for high-speed lookups, I’d use a key-value store like Redis. For flexible structured data with query needs, I’d use a document store like MongoDB. For time-series metrics, I’d pick InfluxDB or Cassandra. The right choice is about matching the database’s strengths to the workload.”

---

If you want, I can also make a **decision table** mapping *use case → best NoSQL type → example DB → SRE relevance*.
That’s the kind of thing interviewers love because it shows you can choose tech pragmatically, not just list names.

Do you want me to prepare that?

