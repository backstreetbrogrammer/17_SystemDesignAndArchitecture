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
3. Algorithms and Data Structures
4. Working with Big Data
5. Design Interview Strategies
6. Mock Design Interviews
7. General Tech Interview Tips

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

