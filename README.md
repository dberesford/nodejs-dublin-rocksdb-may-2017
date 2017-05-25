<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#org257a70d">1. Introduction</a></li>
<li><a href="#org1005ba4">2. Backstory - Flash</a></li>
<li><a href="#orgaa6f297">3. Backstory - latency</a></li>
<li><a href="#orgc7a155a">4. Backstory - latency</a></li>
<li><a href="#org3040600">5. Backstory - no latency!</a></li>
<li><a href="#org5a21db4">6. Backstory - LSM</a></li>
<li><a href="#org33dbb8b">7. Backstory - LevelDB</a></li>
<li><a href="#orgfc17120">8. RocksDB Development in Facebook</a></li>
<li><a href="#orgd6bbe25">9. RocksDB architecture</a></li>
<li><a href="#orgdc0ad37">10. RocksDB what it's not</a></li>
<li><a href="#org8ee34e4">11. Performance</a></li>
<li><a href="#org1f41922">12. Where is it used?</a></li>
<li><a href="#org25f040b">13. Code/Demo</a></li>
<li><a href="#orgfaacae4">14. Where is RocksDB going?</a></li>
<li><a href="#orgc62534a">15. What's the plan for rocksdb-node?</a></li>
<li><a href="#orgebb3656">16. RocksDB &amp; Node.js - Exponential Disruption!</a></li>
<li><a href="#orgf55e588">17. THANK YOU!</a></li>
</ul>
</div>
</div>


<a id="org257a70d"></a>

# Introduction

-   RocksDB Backstory
-   RocksDB & Node.js
-   Code/Demo
-   Disruptions!


<a id="org1005ba4"></a>

# Backstory - Flash

-   Flash - massively disruptive
-   NVM-E arrays mainstream
-   Data migrating
-   SSD 200x improvement
-   Problem: Write amplification
-   Problem: Endurance problems
-   Storage-class memory (SCM)


<a id="orgaa6f297"></a>

# Backstory - latency

![img](./images/fb1.png)


<a id="orgc7a155a"></a>

# Backstory - latency

![img](./images/fb2.png)


<a id="org3040600"></a>

# Backstory - no latency!

![img](./images/fb3.png)


<a id="org5a21db4"></a>

# Backstory - LSM

-   LSM (Log-Structured Merge-tree)
-   Patrick O'Neill Paper 1996
-   BigTable, HBase, Cassandra, Influx
-   Make disk access sequential!
    
    ![img](./images/lsm1.png)


<a id="org33dbb8b"></a>

# Backstory - LevelDB

-   Google - 2011
-   Replacement for SQLite in IndexDB
    
    ![img](./images/leveldb_levels.png)


<a id="orgfc17120"></a>

# RocksDB Development in Facebook

-   Level was evolutionary, but has problems..
    -   Not built for server workloads
    -   Poor performance once db bigger than RAM
    -   Compaction process insufficient
    -   Not optimised for Flash
-   RocksDB
    -   Embedded K/V store with point lookups and range scans
    -   Optimized for fast storage, e.g. Flash and RAM
    -   Server Side database with full production support
    -   Scale linearly with number of CPU cores and with storage IOPs
-   Elegant tradeoffs of read, write & space amplification
    -   i.e. [The RUM Conjecture](http://daslab.seas.harvard.edu/rum-conjecture/)


<a id="orgd6bbe25"></a>

# RocksDB architecture

-   Pluggable architecture
    -   Tunable for different workloads on different hardware
    -   e.g. pluggable compression modules (snappy, zlib, bzip, etc)
-   Level style compaction & 'Universal' style
-   [Features not in Level](https://github.com/facebook/rocksdb/wiki/Features-Not-in-LevelDB)
-   It's not Level any more!

![img](./images/rocks-arch.png)


<a id="orgdc0ad37"></a>

# RocksDB what it's not

-   Not distributed
-   Not fault tolerant
-   Not replicated
-   Not sharded
-   It's an **embedded** database!


<a id="org8ee34e4"></a>

# Performance

-   [Performance benchmarks](https://github.com/facebook/rocksdb/wiki/Performance-Benchmarks)
-   [Replacement for InnoDB](https://code.facebook.com/posts/190251048047090/myrocks-a-space-and-write-optimized-mysql-database/)


<a id="org1f41922"></a>

# Where is it used?

-   MyRocks
-   CockroachDB
-   MongoRocks
-   LinkedIn, Yahoo, Pinterest, Airbnb &&#x2026;


<a id="org25f040b"></a>

# Code/Demo

-   [RocksDB](https://github.com/facebook/rocksdb/wiki)
-   [RocksDB-Node](https://github.com/dberesford/rocksdb-node)


<a id="orgfaacae4"></a>

# Where is RocksDB going?

-   [Very active!](http://rocksdb.org/blog/)
-   [Geo](https://github.com/facebook/rocksdb/blob/master/include/rocksdb/utilities/geo_db.h)
-   [Spatial](https://github.com/facebook/rocksdb/blob/master/include/rocksdb/utilities/spatial_db.h)
-   [Date Tiered](https://github.com/facebook/rocksdb/blob/master/include/rocksdb/utilities/date_tiered_db.h)
-   [JSON Document](https://github.com/facebook/rocksdb/blob/master/include/rocksdb/utilities/json_document.h)


<a id="orgc62534a"></a>

# What's the plan for rocksdb-node?

-   Try support rocksdb API as closely as possible
-   Finish the core RocksDB API
    -   features which require user defined functions
        i.e. Comparators, Filters, Merge Operators, and SliceTransform
-   Move on to the 'utility' APIs
    i.e. Backup, Geo, Spatial, JSON etc
-   Do not go beyond the rocksdb API!
    i.e. this can be done in other modules..


<a id="orgebb3656"></a>

# RocksDB & Node.js - Exponential Disruption!

-   Why write a database in node?
    -   Imagine a world&#x2026;
-   Keep compute close to the data
-   IOT
-   No Caching
-   Analytics
    -   No SQL
    -   ETL & ELT
    -   "Big" data
-   ML
-   [SCS](http://scs-architecture.org/) (microservices are dead!)
-   Polygot persistence
-   More systems, more data, more work 
    -   long long tail


<a id="orgf55e588"></a>

# THANK YOU!

-   twitter: @dberesford
-   <https://github.com/dberesford/nodejs-dublin-rocksdb-may-2017>
-   <http://www.nearform.com/careers/>

