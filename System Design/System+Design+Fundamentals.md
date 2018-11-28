
# System Design Fundamentals

There are more in depth guides/notes out there. These are just reminders of the core principles. You should read up more in depth on topics prior to using this.

Todo:
- REST
- Caching
- Queues + Asynchronism
- Security
- RPC
- CDNs
- Map Reduce
- Case Study on SpatialOS
- Design a couple of things

## Question Answer Approach

1. Use cases, constraints assumptions.
  - Who? How? How many? What inputs? How much data? How many requests per second?
2. High level design.
  - Sketch main components.
3. Design core components (details).
4. Scale
  - LB, Horizontal scaling, caching strategies, DB optimisations
 
## Important concepts
  
### Performance vs Scaling

- Scalability problem - fast for a single user, slow under load
- Performance problem - slow for a single user

- Horizontal Scaling: More boxes
- Vertical Scaling: More resources on a box

### Latency vs Throughput

- Latency - time to perform some action
- Throughput - number of actions we can perform in a unit of time.

### CAP Theorem

- Consistency: Every read gets most recent write or error.
- Availability: Every request gets a response, no guarantee of recency.
- Partition Tolerance: System continues despite network failures.

#### Consistency

- Weak: Best effort. E.g. VoIP or online games.
- Eventual: Asynchronous replication (it'll happen over time)
- Strong: Synchronous, transactional, has to happen before anything can tick.

#### Availability

1. Fail Over
  - Active Passive (heartbeat on a master + awake a backup. Time to wake depends on standby mode - hot or cold.)
  - Active Active (load spread between servers)
  - Disadvantages: More hardware, complexity, risk of loss of data if active system fails before data written to passive.
2. Replication
  - Master/Slave - master writes, broadcasts, slaves read only.
  - Master/Master
  - Disadvantages: Logic needed to promote slaves; Need a load balancer for Master/Master, they are loosely consistent (violate ACID), high write latency for synchronization, sometimes need conflict resolution
  
### SOLID

- Single Responsibility
  - Classes have one job
- Open Closed
  - Open to extension
  - Closed to modification
- Liskov Substitution:
  - A subclass must be substitutable for its superclass
- Interface Segregation
  - Interfaces should be fine grained + specific
- Dependency Inversion
  - High level module should not depend on low level module
  - Abstractions should not depend on details
  
### Load Balancers

- Distribute requests from clients to servers
- Prevent requests going to unhealthy servers
- Prevent overloading a single resource
- Eliminates single point of failure
- Can have multiple with fail over availability
- SSL termination

Strategies:

- Random
- Least Loaded
- Session-based
- Round Robin
- Layer 4 (IP, ports etc.)
- Layer 7 (message, cookies, header)

Disadvantages:

- Can be a bottleneck.
- Can be a single point of failure, having multiple increases complexity

### Reverse Proxies

- Web server that centralizes internal services.
- Better security, can obfuscate server info, blacklist IPs, limit connections per client
- Better scalability/flexibility - clients only see reverse proxy, you can do whatever you like with servers behind the scenes.
- SSL termination
- Can compress server responses
- Can serve assets statically
- Can act as a cache

Disadvantages:

- You guessed it, single point of failure, having multiple = increased complexity

#### LBs vs RPs

- Load balancer -> Helpful with multiple servers
- Reverse Proxies -> Can be helpful with just one server
- NGINX can do both

## Databases

### RDBMS

Relational DBS are ACID:

- Atomic: Every transaction is all or nothing.
- Consistent: Any transaction takes db from one valid state to another.
- Isolated: Executing transactions concurrently == executing transactions serially.
- Durable: Transactions stay once they are done.

We've discussed replication techniques. Make sure you brush up on advantages/disadvantages from a db perspective.

#### Partitioning Technique: Federation

Split DBs up by *function*. I.e. instead of monolithic DB, you have 3 micro DBs that have specific roles -> less traffic + less replication lag as a result. Better cache locality, better throughput.
BUT: DB Joins are fucked, necesary to update application logic to deduce which DB to read + write, more hardware etc.

#### Partitioning Technique: Sharding

Distribute data across DB shards, which form a cluster. Same advantages of federation.
Other disadvantages, however, include lopsided data distribution, rebalancing is hard.

#### Redundancy Technique: Denormalization

Attempts to improve read performance at expense of write performance. Write redundant copies of data into multiple tables to avoid expensive DB joins. Can help in managing Federation/Sharding. 
Disadvantages include duplicated data, more complexity to keep info in sync, under heavy write load it'll go tits up.

### NoSQL

Key-value store, with no real relations.  Denormalized, joins done in application code. Follows BASE:

- Basically available: Guarantees availability
- Soft state: State may change over time, even without input
- Eventual consistency: System will become consistent over a period of time if it receives no input during that period.

#### SQL VS NOSQL

Use SQL when:

- Structured Data
- Strict Schema
- Relational Data
- Complex joins
- Transactions
- Clear scaling patterns

Use NoSQL when:

- Semi structured data
- Flexible/dynamic schema
- Non-relational data
- No joins
- TB or PB of data (bigtable)
- Data intensive workload


```python

```
