### Sharding

- Why do we need it?
- When dealing with large databases, if theres only one server, then querying from that server is a very slow operation leading to the reqt of more memory, more CPU (even if we have indexes)
- row based partitioning (lets say 1 million rows into 5 DB instances) on a key (shard key)


- HP vs sharding
    - HP splits big table into multiple tables in the same DB
    - Sharding splits big table into multiple tables across multiple database servers

    - HP table name changes (or schema)
    - Sharding everything is same but server changes

    - HP: same DB, multiple tables; Sharding: multiple DBs

- Sharding demo
    - Make 3 shards using docker

    Source Code
    https://github.com/hnasr/javascript_playground/tree/master/sharding

    Docker commands (including pgadmin)
    https://github.com/hnasr/javascript_playground/blob/master/sharding/shards/commands.txt

    Dockerfile & init.sql
    https://github.com/hnasr/javascript_playground/tree/master/sharding/shards

- Pros
    - Scalability: for both data and memory
    - Security: A particular shard is accessible to certain people refraining them to access the other shards
    - Optimal and smaller index size

- Cons
    - Complex client (whos aware of the shard)
    - Transactions across shards is a problem
    - Rollbacks are very hard in case a transaction fails
    - Joins are hard to implement as tables are across servers
    - It is an expensive operation when someone searches for something since the user doesnt have the key, the scan is to be performed across all the shards

### NOTE:
- In case to make reads faster, we can use horizontal partitioning which is automatically done by the DB if you set it on
- Logic is in client's app (sharding)
- When should we consider sharding?
    - when we want to scale the writes
    - take the case of youtube

- Learn about Vitez