**suppose in case you have db which has too many records and you are having performance issue now.what are steps you will start in to 
to resolve the performance issues?**
------------------------------------------------------------------------------------------------------------------

1. Identify the Root Cause
Use App dynamics or TOAD monitoring tools to check where is the issue.
2. Check the slow queries
3. Check the explain plan for the queries with heavy result.
4. Avoid any subqueries
5. Optimize queries like avoid select *, avoid subqueries , use proper indexing 
6. Optimize the database design like perform normilization and denormalization
7. Archive old legacy data in separate table and enable new data to new table
8. Use caching to avoid everytime hit to DB.
9. Efficiently use the database connection pooling

**Can a single instance of DB server can lead to performance issues?**
----------------------------------------------------------------------
1.Use distributed DB
2.Use cloud managed DB for managing auto scaling in case of high loads.
3.Add read replicas, use load balancing




**what is distributed database?**
---------------------------------
Distributed database is where we have data lying in multiple physical locations.
These locations could be on the same network or spread across different geographical regions
Despite being distributed, the database appears to users as a single, unified system.
Database is distributed in multiple nodes, if one node fails then request will land to other nodes.
Database replication is the process of copying and maintaining database objects (like tables, schemas, and 
transactions) from one database (the source) to another (the replica). The goal is to ensure that multiple 
databases stay in sync, improving availability, performance, and fault tolerance.

**Why Use Replication?**
------------------------

✅ High availability: If one server fails, others can still serve data.
🚀 Faster read performance: Distribute read traffic across replicas.
🌍 Geographic distribution: Place data closer to users in different regions.
🛡️ Disaster recovery: Replicas can act as backups in case of failure.

