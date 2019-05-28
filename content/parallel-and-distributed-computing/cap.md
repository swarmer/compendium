+++
title = "CAP Theorem"
weight = 1
sort_by = "weight"
+++


CAP theorem states at any given moment a distributed system can satisfy no more than 2 out of 3
requirements:
- Consistency
- Availability
- Partition Tolerance


## Consistency

This property requires that the distributes system conforms to the linearizable consistency model:
any read must return the latest finished write.


## Availability

This property requires that every request received by a non-failing node results in a sensible
response without blocking indefinitely.


## Partition Tolerance

If a network is in a state of partition, this means that an arbitrary number of messages can be
dropped or delayed for an arbitrary amount of time.

Partition tolerance means *having to operate in presence of network partitions*, without specifying
how successfully a system must operate.

Note that this badly named property doesn't mean that the system must work or be available in the
presence of network partitions: a CP system despite having "partition tolerance" among its
properties may just shut down and be unavailable.


## Clarification

Since any real-world network may fail, network partitions are always possible, and a system cannot
forgo the "Partition Tolerance" property at all times. Therefore, distributed systems that are
generally CA are not possible. The only way for a system to always be CA is to not be distributed
and consist of a single node.

However, a system may choose to provide different guarantees in presence of partitions and
otherwise. It would then make sense to describe systems by a pair of property sets, such as:
- CA/CP: a system provides both consistency and availability when the network is fully operational,
  but under a partition it drops availability and may reject requests to preserve consistency.
- CA/AP: a system provides both consistency and availability when the network is fully operational,
  but under a partition it still serves all requests while not preserving consistency.
- A/AP: a system that never tries to provide consistency, even when not under a partition.
- CA/P: a system provides both consistency and availability when the network is fully operational,
  but under a partition some or all nodes may be unavailable, *and* consistency is also not
  maintained.

The authors of Spanner by Google talk about the possibility of a system being "effectively"
(but not technically) CA, meaning that they achieved such a high level of reliability in their
networks that partitions happen more rarely than other types of errors, such as:
- bugs in the system software
- system operator errors
- user errors
- non-network hardware failures

In this case the behaviour of the system under partitions becomes less significant, but it should
still be specified in rare cases when network partitions do happen anyway (Spanner chooses
consistency in these cases, meaning that it's a CA/CP system under the terminology defined above).
  