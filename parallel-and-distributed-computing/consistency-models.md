# Consistency Models

_Disclaimer: this is compiled on a best effort basis from a lot of confusing, incomplete and sometimes mutually exclusive sources, so correctness is not guaranteed._

For the sake of performance and/or scalability, modern computing is usually separated into a number of parallel processes:

* different units within one cpu core
* multiple cores within one cpu
* multiple cpus in one computer
* multiple processes in one OS
* multiple computers/nodes in one cluster

Often a set of parallel processes forms a high level abstraction, such as a database, that hides the fact that it's really a bunch of nodes each having its own copy of some or all stored data. Instead this abstraction presents a single unified view of data stored inside, as if it was in one place. However this illusion is never perfect: to gain any value from distributing system in multiple nodes we have to forgo some of the guarantees that we are used to when dealing with single-threaded systems. We then need a way do describe the guarantees that are left to keep a way to reason about the possible results of working with a distributed system.

A **consistency model** is a set of rules that precisely describe allowed results of series of operations performed on such distributed system in parallel.


## Single-object, single-operation models

These models only describe rules concerning series of singular ungrouped operations on singular ungrouped objects. An object can be a location in memory, a more complex structure such as a queue, or even something larger.


 
### Strict Consistency

Strongest model: all writes appear to happen instantenaously at the exact time they are issued [when they are finished in some sources]. Any read of a variable must return the value of the most recent write on this variable. It's what you might intuitively want, but this might only hold when you are dealing with a single-threaded system. The reason why this is not possible to implement otherwise is that write operations in real distributed systems *take time*. Physics and the speed of light put a lower bound on how quickly information can propagate from one node to others. In practice networking hardware (or really all hardware along the way) introduces additional significant latency.


### Linearizability (Strong Consistency)

This model includes the fact that operations take time: each operation is defined to have a start time when it's invoked, and an end time when it's acknowledged. Linearizability guarantees that each operation appears for all  processes to happen atomically at a single instant sometime between it's invocation and its acknowledgement. This implies that like in sequential consistency, described below, all processes agree on the order of operations and that operations made from one process are seen by other processes in correct program order. Unlike in strict consistency, operations don't need to be applied in the order of their starting points in time.

Linearizability has a property of being *local*, meaning that combining a system, linearizable with respect to singular objects in it with another such system will produce a combined system that is also linearizable with respect to singular objects of original systems. However to the best of my knowledge it is not guaranteed to be linearizable with respect to groups of original objects or composite objects.


### Sequential Consistency

Sequential consistency drops the requirement that an operation takes effect between its invocation and acknowledgement. Instead, for instance, a read can "take effect" before its invocation, meaning it is stale, a write can be queued to take effect after its acknowledgement, meaning that it may not yet be visible at the end of operation, etc. This can be thought of as an asynchronous version of linearizability.

It's still required that all processes (eventually) see  operations performed in a single order in which operations performed by a particular process are not reordered between each other.


### Causal Consistency

Instead of sequential consistency's requirement that the order of *all* operations by a process is preserved, we can only require that the order of *causally related* operations is preserved. Causal relations can be defined in different ways and these relation can be explicitly specified when invoking them.


### Eventual Consistency

A weak model specifying that in absence of updates to an object, all nodes will converge to the same state and all reads on this object will return the latest written value.


## Multi-object, Multi-operation Models

These models come from databases background and include a concept of transaction containing multiple operations on a number of objects.


### Strict Serializability

A version of serializability that additionally guarantees that their execution is as if the transactions' order in real time was preserved.


### Serializability

A guarantee that a result of execution of several transactions' operations could have been produced by executing these transactions one at a time, one after another in some arbitrary order.


### Repeatable Read

After a transaction has read certain rows, on subsequent reads these rows will not be changed, even if another transaction changed them and committed. Phantom reads — reads returning a changed set of rows that satisfy a search confition are allowed according to the SQL standard.


### Read Committed

A transaction will never read uncommitted data, but it may re-read data previously read and get changed rows, updated by other recently committed transactions.


### Read Uncommitted

A transaction will see all updates, even not yet committed.

  