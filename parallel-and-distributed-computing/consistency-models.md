# Consistency Models

For the sake of performance and/or scalability, modern computing is usually separated into a number of parallel processes:

* different units within one cpu core
* multiple cores within one cpu
* multiple cpus in one computer
* multiple processes in one OS
* multiple computers/nodes in one cluster

Often a set of parallel processes forms a high level abstraction, such as a database, that hides the fact that it's really a bunch of nodes each having its own copy of some or all stored data. Instead this abstraction presents a single unified view of data stored inside, as if it was in one place. However this illusion is never perfect: to gain any value from distributing system in multiple nodes we have to forgo some of the guarantees that we are used to when dealing with single-threaded systems. We then need a way do describe the guarantees that are left to keep a way to reason about the possible results of working with a distributed system.

A **consistency model** is a set of rules that precisely describe allowed results of sequences of operations performed on such distributed system.


## Strict Consistency

Strongest model: all writes appear to happen instantenaously at the exact. Any read of a variable must return the value of the most recent write on this variable. It's what you might intuitively want, but this might only hold when you are dealing with a single-threaded system. The reason why this is not possible to implement otherwise is that write operations in real distributed systems *take time*. Physics and the speed of light put a lower bound on how quickly information can propagate from one node to others. In practice networking hardware (or really all hardware along the way) introduces additional significant latency.


## Linearizability
This model includes the fact that operations take time: each operation is defined to have a start time when it's invoked, and an end time when it's acknowledged. Linearizability guarantees that each operation appears for all  processes to happen atomically at a single instant sometime between it's invocation and its acknowledgement. This implies that like in sequential consistency, described below, all processes agree on the order of operations and that operations made from one process are seen by other processes in correct program order.