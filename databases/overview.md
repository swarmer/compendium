# Overview

## CODASYL Data Model

A common standard interface, published in 1969, for access to databases supporting
network data model using tuple-at-a-time queries. These databases give developers precise low-level
control of data representation. One disadvantage is that the format of data storage is a part of
public API and is impossible to change without rewriting client code. Another disadvantage is that
network data model causes complex queries such as manually joining data using nested for loops.


## Relational Databases

Published in 1970 by Edgar Frank "Ted" Codd, designed to abstract away physical data representation
and instead present a high-level relational interface to access data as a set of tables.


## Object databases

An attempt to avoid object-relational impedance mismatch, they store objects directly.
Main downsides are a lack of a single expressive query language and inability to use from different
programming languages.


## Analytical Relational Databases

Databases specifically build to run OLAP (analytical) workloads efficiently. Don't support
OLTP (transactional) workloads well, which is worked around by transferring slightly stale data
from the main transactional database and using the analytical database purely for analytics.
The main way to gain performance is by using columnar storage.


## NoSQL

A loose movement of databases deciding to forgo the relational model, SQL and ACID principles to
more easily achieve high performance and scalability by sharding. Another common characteristic
is lack of schemas.


## NewSQL

A new generation of relational databases supporting SQL that attempt to achieve scalability and
performance on transactional workloads that are comparable with those of NoSQL databases.

A big trend among modern databases is ability to support hybrid (HTAP) workloads.
