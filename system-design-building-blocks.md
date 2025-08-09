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
