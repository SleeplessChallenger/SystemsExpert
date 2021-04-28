**Replication And Sharding**

Database(s) are critical to many systems, hence availability of them is essential. 

**Replication** - copy of your current (main) db. When the main db falls down, the replica takes over and <ins><i>becomes the new main db</i></ins>. And if the crashed one gets recovered, it gets data from <i>‘former replicated and new main’</i> and becomes again main db. That’s why every operation on main db should be **replicated in sync** with replica db. => write operations will take longer.
<br>
**Note:** if write operation fails on replica, then it must be rollbacked on main db as well. 

But if we have DBs located in various parts of the world [and they’re located in various parts of the world to enable low latency] , then **async replication**, to update DBs in various parts of the world, may be an option to improve latency <i>(if strong consistency/no staleness of the particular element in the system isn’t required)</i>

If we have one DB => eventually it gets overloaded. Then we can vertically scale it, but there is limit. Hence, horizontal scaling is an option (increase amount of DBs). But what if we split up data as our system has tons of data?
One part of data will be stored in one db server, another part in another server. - **sharding** <br>
**Sharding** - process of splitting/partitioning your main db (data) into smaller parts, called <ins>shards/data partitions</ins> => throughput increased <br>
**Ex:** take payment relational database. Payments whose customer name starts with A-I goes to shard one, from F-J to shard 2 etc. Or we can do it based on customer’s region.

But above mentioned way may lead to **hot spots** - uneven spread of data across servers. To deal with it we can use **hashing function**. In regard to way of organizing: either of the 2 hashing strategies isn’t an option [i.e. Consistent: of course, if one of the servers (db) fails, the amount of data migration lesser the bigger number of servers (db), but db is critical, hence we can’t lose it], maybe, and **replicas** of shards may be an option. <br>
**Ex:** Client makes request about the data to the server. Server has some logic which will decide which shard (DB) to direct the request. <br> 
**But:** it’s way better to have Reverse Proxy **after the Server**. This reverse proxy will decide which shard (db) take data from. Decision can be made by hash function to enable uniformity, for example.

![Alt text](ImageRepo/Replication_And_Sharding.png?raw=true)
