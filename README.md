# System Design And Architecture

> Organizing components structures and behaviors for any simple to complex system.

Systems design interfaces, and data for an electronic control system to satisfy specified requirements. System design
could be seen as the application of system theory to product development.

## Table of contents

1. Scalability
    - Single Server
    - Separating out the database
    - Vertical Scaling
    - Horizontal Scaling
2. Fail-over Strategies
    - Cold Standby
    - Warm Standby
    - Hot Standby
3. Sharding Databases
4. Algorithms and Data Structures
5. Working with Big Data
6. Design Interview Strategies
7. Mock Design Interviews
8. General Tech Interview Tips

### Youtube

![System Design](SystemDesign.png)

---

### Chapter 01. Scalability

#### Single server

Maintain a single server - mainly an HTTP server to service clients web requests.

![Single Server](SingleServer.PNG)

Disadvantage: Single point of failure.

#### Separating out the database

By separating out the database from the web server node, we can scale both web server node and database node
independently. However, there is still a single point of failure.

![Single Server with Database](ServerWithDB.PNG)

#### Vertical Scaling

It is defined as the process of increasing the capacity of a single machine by adding more resources such as memory,
storage, etc. to increase the throughput of the system. No new resource is added, rather the capability of the existing
resources is made more efficient.

Example: `MySQL`

![Vertical Scaling](VerticalScaling.PNG)

However, there is still a single point of failure. Also, there is a limit to the capacity of a single machine.

#### Horizontal Scaling

It is defined as the process of adding more instances of the same type to the existing pool of resources and not
increasing the capacity of existing resources like in vertical scaling. This kind of scaling also helps in decreasing
the load on the server.

![Horizontal Scaling](HorizontalScaling.PNG)

In this process, the number of servers is increased and not the individual capacity of the server. This is done with the
help of a **Load Balancer** which basically routes the user requests to different servers according to the availability
of the server. Thereby, increasing the overall performance of the system. In this way, the entire process is distributed
among all servers rather than just depending on a single server.

Example: NoSQLs like `Cassandra` and `MongoDB`

![Load Balancer](LoadBalancer.PNG)

All the nodes are "**stateless**" meaning that each node doesn't maintain the state of client requests. In other words,
any node can serve client request without maintaining the state => however, the database can store all the clients
request and service states.

So we should choose vertical scaling or horizontal scaling based on the system architecture (big or small), user base,
web traffic expected etc.

![Vertical Scaling Vs Horizontal Scaling](VerticalScalingVsHorizontalScaling.PNG)

---

### Chapter 02. Fail-over Strategies

#### Servers are provisioned as:

- Own company's data centers
- Cloud services: Amazon EC2, Google Compute Engine, Azure VM's, etc.
- Fully managed "serverless" services: Lambda, Kinesis, Athena, etc.

#### Failover servers: Cold Standby

Periodic backup of data is done on the current primary server. The storage device can be anything like external hard
disk, magnetic tape, etc. Once the current primary server goes down - the standby server is "prepared" to be in same
state as primary from the backup storage.

Drawback: may take time to prepare the standby server and data will be lost during this time.

#### Failover servers: Warm Standby

Instead of doing periodic backup, we can replicate data in realtime. Data replication is already available in major
databases which will automatically sync up the data to standby server in realtime.

#### Failover servers: Hot Standby

Servers can directly write to all the different databases (primary, secondary, etc.) in a distributed fashion.
Similarly, the servers can also do distributed reads from all the databases. Thus, any failure of a single database host
will have minimal impact on data loss.


---

### Chapter 03. Sharding Databases

Database sharding is a type of horizontal partitioning that splits large databases into smaller components, which are
faster and easier to manage. A shard is an individual partition that exists on separate database server instance to
spread load. Auto sharding or data sharding is needed when a dataset is too big to be stored in a single database.

As both the database size and number of transactions increase, so does the response time for querying the database.
Costs associated with maintaining a huge database can also skyrocket due to the number and quality of computers we need
to manage our workload. Data shards, on the other hand, have fewer hardware and software requirements and can be managed
on less expensive servers.

![Database Sharding](DatabaseSharding.PNG)

Based on some data field or hash key, shards can be selected and stored the data into. Each shard also replicates the
data to other shards for hot standby fail-over recovery.

![Hash-Based Sharding](HashBasedSharding.PNG)

