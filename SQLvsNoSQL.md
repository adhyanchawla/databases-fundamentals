Databases Fundamentals

SQL vs NoSQL

SQL

- Structure
    - stored in tables (rows & columns), relations between different tables
    - predetermined schema
    - internally data may or may not be stored in B+ trees (logN) lookup, just cuz innoDB is used as a storage engine, a lot of people think that its stored in the form of B+ trees
    - one single row is stored in a single B+ tree node

- Nature
    - concentrated/centralised across a single server (means tables wont be broken down into smaller tables by row or columns over multiple servers)

- Scalability
    - Vertical (increasing more power i.e. RAM size, storage capacity)
        - fits better to SQL
    - Horizontal (sharding i.e. distributing data across more servers)
        - data can be dirtributed across servers (not supported well here)

- Properties (ACID Data integrity)
    - supported by SQL
    
NoSQL
- Structure
    - Unstructured data (key-value, document, column-wise, graph) --- types of DBs (there is no sanitization)
        - Key value DB - 
            - eg key | value
                    1 | (Integer, String)
            - value part is opaque -- you cannot query on the basis of the values, searching only on the basis of the key
            - fast in nature
        - Document DB
            - eg. Key | Value
                    1 | (JSON, XML)
            - value part is not opaque in this case (difference from key value DB) -- search on the basis of key as well as query on the basis of value is allowed
            - eg Mongo DB uses wired tiger storage engine, implemented much similar to relational DBs
            - eg in Mongo DB data is stored in the form of BSON
            - 1 document in binary encoded form is stored in B+ tree
        - Columnwise DB
            - eg. Key ----> Column A vs Value A, column B vs Value B, and so on
                    1 ----> first_name vs Adhyan, last_name: Chawla, age: 23
                    2 ----> first_name vs Raj, dept_name: IT
        - Graph DB
            - eg. like in graphs, we have nodes and edges, that means there is a relationship between two nodes incase there is an edge
            eg. social networking, recommendation

- Nature
    - No relations between the data of two nodes (decentralized)
    - Distributed in nature

- Scaling
    - Vertical
        - not preferred here
    - Horizontal
        - visible here

- Properties (BASE)
    - Basically available (highly available DB - data in distributed manner - replication available - if one failover - one can use it from the other server)
    - Safe state (state of data can be changed without any user interaction)
    - eventual consistency (retrieval of stale data at one point of time, data gets updated after sometime)

Why SQL and NoSQL
- Flexibility is more offered by SQL as compared to NoSQL as it supports queries and NoSQL supports only basic queries. In NoSQL, in advance, what columns you need to search (capability)
- Relational data in case of SQL whereas Tightly bound data in NOSQL
- Data integrity (ACID) followed by SQL and not by NoSQL. NoSQL is used for BigData (millions of data) when there is a need for realtime data - eg. messaging apps uses NoSQL
- Availability - high availablity, performance with some inconsistency, go for NoSQL
- Joins - on a distributed database is expensive because you have to run data over a network, for joining two tables in separate machines, the data needs to be present in some common machine
with sharded database, one has to pull all the data in a common place which is an expensive step
in relational databases, the tables are present on a single node
- Replication - is the same (better to use asynchronous mechanism for reads so that you dont highly depend on master db)

