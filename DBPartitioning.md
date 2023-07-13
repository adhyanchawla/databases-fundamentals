Partitioning of a database

- What is partitioning? Why does it exist?

- Scanning through the entire table is an expensive operation if lets say you have 1 billion rows. you cant afford to wait for such an iteration and response returning to you after a while
- instead you partition the table i.e. break the table into smaller tables and each table lets say have 2,00,000 rows
- when we query, with a WHERE clause then the database knows which table to extract the rows from and return the results in no time

- Horizontal vs vertical partitioning
    - Horizontal partitioning (generally preferred)
        - splitting rows into partitions
    - Vertical partitioning
        - splitting columns into partitions with entire row
        - eg used when lets say you have a large column having blob and you rarely query that blob
        - you dont want the blob to take up space or prohibit you from fast access
        - attach to the master table thereby allowing only the fast access columns to store in a SSD

- Partitioning types (client is agnostic, doesnt care on what basis is the partition done)
    - Partition can happen via:
        - By range i.e. dates, ids e.g. logDate or customerId (from this date to this date)
        - By list i.e. discrete values eg (states like CA) or zip codes
        - By Hash (consistent hashing) 
            - eg cassandra uses consistent hashing
            - in proxies, we use IP hash (which backend to hit based on the IP)

- Partitioning vs Sharding
    - Taking horizontal partitioning into consideration
    1. HP splits the big table into multiple tables in the same DB and DB takes care of management of data where Sharding splits the big table into multiple tables across servers 
    Sharding is done to reduce the latency for eg California customers data will be added to a DB server in Cali... the request from Cali customers will hit the proxy and it will identify the IP address of the user and hence, it will serve you to the database instance related to Cali
    2. HP table name changes but in sharding table name remains the same but server changes

- Demo
<!-- TODO: ADD images/queries in postgres in docker  -->

- Pros and Cons
    - Pros:
        - Improves the query performance when accessing a single partition
        - seq. scan vs scattered index scan
            - scattered index scan slower in this case
            - sequential faster
        - easy bulk loading. eg create a replica of the master table and attach partition to that table
        - archive old data that are barely accessed into cheap storage

    - Cons:
        - Updates that moves rows from partition to another is slow and not recommended as it will take toll over the RAM and the update might fail at times
        - inefficient queries could scan all the partitions resulting in slower performance (select * from table)
        - schema changes are challenging (DBMS does it usually) i.e. indexing on the master table will reflect the indexing on the child table
