# In-memory Databases

Notes about implementation of efficient in-memory databases running on multi-core systems.


## Overview

Traditional disk-oriented databases assume that most of their data will not fit into RAM and a large
portion of data accesses will have to read data from slow disks. However modern machines can have
terabytes of RAM in them, which is enough to completely contain a very large portion of datasets.
In this case the architecture of disk-oriented databases becomes suboptimal because they perform
a large amount of unnecessary work (such as keeping track of and locking data pages) and pay little
attention to previously insignificant concerns such as fast synchronization primitives,
cache friendliness etc.

Using mmap to automatically page memory in a out to disk also appears suboptimal because the data
representation on disk has to be the same as in memory, and also because the database system loses
precise control and knowledge of whether pages are in memory and whether they are accessed
asynchronously.


## Data organization

Instead of finding records by special ids, database systems can in some cases store direct pointers
to wherever targer records are stored in memory, removing a level of indirection. It's also easier
to have separate memory pools for fixed-length columns and variable-length columns of different
sizes.


## Concurrency control

Since the cost of accessing a row is now comparable to the cost of acquiring a lock, it may be
worthwhile to use more coarse-grained locking to acquire less locks, particularly in sequential
scans. Other ways to optimize concurrency control are storing lock together with related data
for better cache locality, and using atomic processor instructions instead of more heavyweight
mutexes.


## Indexes

Since building an in-memory index from in-memory data can be done much quicker than before, it's
common to just rebuild them on restart to avoid runtime overhead of logging.


## Query Processing

The optimal query plans change in in-memory databases: for instance, random access patterns become
closer to sequential access in performance.

The overhead of a tuple-at-a-time iteration model becomes too high and instead it's more optimal
to iterate over fixed-size chunks of tuples.


## Logging and Recovery

Just as before, performing a group commit (batching multiple log entries into a single fsync) is an
important way to reduce time spent in fsync.

Since we never need to swap out dirty pages to disk to conserve memory anymore, we can guarantee
that snapshots written to disk never contain any uncommitted data and so there's no need to
undo log entries (and log them at all) after crashes.

Saving checkpoints to disk is simplified by the fact that all data is now in address space of the
process, so it's sufficient to *fork* to get an immutable snapshot of data, while the original
process is free to proceed with its own version of data.
