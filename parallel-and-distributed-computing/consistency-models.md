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

Strongest model: all writes appear to happen instantenaously right when they are issued. Any read of a variable must return the value of the most recent write on this variable.

