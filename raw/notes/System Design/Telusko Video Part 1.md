source: https://youtu.be/Vnm-ycSfJx4?si=3uHFLfIs_Rz8F-c4
## What is a System?

A **System** is a collection of components working together to achieve a common goal.

**Formula:**

```
System = Components + Common Goal
```

---

# Alien Bank Example (Understanding System Design)

## Initial Architecture

### Components

- 1 Cash Counter
    
- 1 Cashier
    
- Multiple Customers
    

### Customer Flow

1. Customer visits counter.
    
2. Deposits or withdraws money.
    
3. Receives receipt.
    
4. Leaves.
    

This simple flow is used to introduce core system design concepts.

---

# Issue 1: Slow Processing

### Problem

- Cashier takes **10 minutes/customer**
    
- Only **6 customers/hour**
    

### Bottlenecks

- Understanding customer request
    
- Manual cash counting
    
- Preparing receipts
    

### Solution

Improve the cashier's efficiency:

- Better training
    
- Faster cash counting
    
- Faster typing
    

### Result

Processing time:

```
10 min → 5 min/customer
```

### System Design Analogy

This is equivalent to:

- Better algorithms
    
- Better code quality
    
- Low Level Design (LLD)
    
- Data Structures & Algorithms (DSA)
    

---

# Issue 2: Growing Customer Traffic

### Problem

Customer count increases rapidly.

The cashier is already optimized.

### Solution

Improve infrastructure instead of the person.

Examples:

- Larger counter
    
- Cash counting machine
    
- Pre-filled forms
    

### Result

Processing time:

```
5 min → 3 min/customer
```

### System Design Concept

**Vertical Scaling**

Upgrade the existing server by adding more resources.

Examples:

- More RAM
    
- Faster CPU
    
- Better SSD
    

---

# Issue 3: Customers Still Waiting

Even after optimization:

One counter processes one customer every 3 minutes.

The 10th customer still waits about 27 minutes.

### Solution

Add another counter.

```
Counter 1
Counter 2
```

### System Design Concept

**Horizontal Scaling**

Instead of upgrading one server,  
add more servers.

---

# Issue 4: Data Inconsistency

With two counters:

Each counter maintains separate data.

Problems:

- Counter 2 doesn't know customer history.
    
- Customer can withdraw twice.
    
- Data becomes inconsistent.
    

### Solution

Use a **Centralized Database**

```
Counter 1
       \
        Database
       /
Counter 2
```

### Benefits

- Shared customer data
    
- Consistent balance
    
- Single source of truth
    

---

# Issue 5: Uneven Traffic

Customers naturally go to Counter 1.

Counter 2 stays idle.

### Solution

Introduce a **Middleman**

The middleman:

- Monitors queue sizes
    
- Sends customers to the least busy counter
    
- Detects failed counters
    
- Redirects traffic
    

### System Design Concept

**Load Balancer**

Responsibilities:

- Distribute requests evenly
    
- Perform health checks
    
- Route traffic away from failed servers
    

---

# Mapping the Bank Example to System Design

|Bank|System Design|
|---|---|
|Customers|Requests / Traffic|
|Queue|Incoming Traffic|
|Cashier|Application Code|
|Cash Counter|Server|
|Shared Records|Centralized Database|
|Middleman|Load Balancer|

---

# Scaling Summary

## 1. Code Optimization

Improve software.

Equivalent to:

- Better algorithms
    
- Better implementation
    
- Efficient code
    

---

## 2. Vertical Scaling

Upgrade existing server.

Example:

- More CPU
    
- More RAM
    
- Better hardware
    

Limit:  
Eventually reaches maximum capacity.

---

## 3. Horizontal Scaling

Add more servers.

Benefits:

- Higher throughput
    
- Better availability
    
- Handles more users
    

Requires:

- Shared database
    
- Load balancer
    

---

# Core Components of System Design

## 1. Database

Purpose:

- Store data
    
- Retrieve data
    
- Update data
    
- Delete data
    

Types:

- SQL
    
- NoSQL
    

---

## 2. Application Layer (Backend)

Purpose:

- Hide database complexity
    
- Expose APIs
    
- Apply business logic
    

Provides endpoints such as:

- GET
    
- POST
    
- PUT
    
- DELETE
    

---

## 3. Client Application

Examples:

- Web app
    
- Mobile app
    
- Desktop app
    
- ATM
    

Communicates with backend APIs.

Architecture:

```
Client
   ↓
Backend API
   ↓
Database
```

---

## 4. Cache

Purpose:  
Store frequently accessed data.

Benefits:

- Faster responses
    
- Fewer database queries
    
- Lower latency
    

Architecture:

```
Client
   ↓
Backend
   ↓
 Cache
   ↓
Database
```

---

## 5. Load Balancer

Used when multiple servers exist.

Responsibilities:

- Health checks
    
- Even request distribution
    
- Failover
    

Architecture:

```
Clients
    ↓
Load Balancer
   ↙      ↘
Server 1  Server 2
```

---

## 6. Message Queue

Used for asynchronous communication between services.

Example:  
Order Service → SMS Service

Instead of waiting for SMS:

```
Order Service
      ↓
 Message Queue
      ↓
 SMS Service
```

Benefits:

- Decouples services
    
- Handles retries
    
- Improves reliability
    
- Supports asynchronous processing
    

Examples:

- RabbitMQ
    
- Apache Kafka
    
- Amazon SQS
    

---

## 7. Monitoring & Logging

Purpose:

- Monitor system health
    
- Detect failures
    
- Track errors
    
- Debug issues
    
- Measure performance
    
- Verify new releases
    

Monitors:

- Servers
    
- Databases
    
- Load balancers
    
- APIs
    
- Message queues
    

---

# Overall Architecture

```
           Client
              │
              ▼
       Load Balancer
         │       │
         ▼       ▼
     Server1   Server2
         │       │
         └───┬───┘
             ▼
          Cache
             │
             ▼
         Database
             │
             ▼
      Message Queue
             │
             ▼
     External Services
        (SMS, Email, etc.)

      Monitoring & Logs
         (Across All)
```

# Key Takeaways

- A system is **components working toward a common goal**.
    
- Optimize **code first**, then **hardware**, then **scale horizontally**.
    
- Horizontal scaling requires **shared storage** and **load balancing**.
    
- Core system design building blocks:
    
    1. Database
        
    2. Backend/API
        
    3. Client
        
    4. Cache
        
    5. Load Balancer
        
    6. Message Queue
        
    7. Monitoring & Logging