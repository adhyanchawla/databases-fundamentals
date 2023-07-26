### Replication

Replication in databases involve sharing info as to ensure consistency between redundant database instances in order to improve reliability, making them more fault tolerant, accessibility in databases

- Master/(Standby/Backup) Replication
    - one master/leader node that accepts writes/ddls
    - one or more backup or standby nodes which are connected to master via tcp connection receives those writes from the master
    - simple to implement no conflicts

- Multi Master Replication
    - Multiple master/leader nodes that accept writes/ddls
    - one or more backup or standby nodes which are connected to master via tcp connection receives those writes from the masters
    - need to resolve conflicts as its a complex approach

- Synchronous/Asynchronous Replication
    - Synchronous Replication - A write transaction to the master will be blocked until it is written in the standby/backup nodes
    eg First 2, First 1, any
    - full consistency

    - Asynchronous Replication - A write transaction is considered as successful if it is written to the master and asynchronously the writes are applied to the backup nodes. (work done in background)
    - eventual consistency

    - People usually prefer first one

- Demo

- Pros
    - reads are scalable (horizontal partitioning)
    - region based queries - DB per region

- Cons
    - Eventual consistency
    - slow writes (syunchronous)
    - complex to implement(multi master)
