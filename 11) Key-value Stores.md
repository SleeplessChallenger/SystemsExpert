**Key-value Stores**

If structure imposed by relational db is cumbersome, then NoSQL db is an option. One of the most popular types of NoSQL db is **Key-Value store**. It allows to map key with particular value.
Example of which can be seen below. It may somewhat resemble hashtable.
**Ex:** <ins><i>caching</i></ins> can use key-value db as it’s pretty convenient because you access them via hash or IP address/username; for <ins><i>dynamic configuration</i></ins>  

In many cases <ins><i>low latency</i></ins> and <ins><i>increased throughput</i></ins> is the result of NoSQL db due to key-value feature

![Alt text](ImageRepo/Key_value_Stores_first.png?raw=true)

![Alt text](ImageRepo/Key_value_Stores_second.png?raw=true)

Difference between those NoSQL DBs? 
 a) some of them write data to disk and even if the key-value store server crashes the data will persist on the disk. Others write to memory (i.e. Redis, but can be implemented as separate entity and if server crashes => data in DB persists) => data will be lost if the server goes down.<br>
 For example, for cache memory writing will be enough<br>
 b) Strong consistency vs Eventual consistency 


Also, if you look at photo below, on line 22 you’ll see **‘EX’** key. It means that our key-value pair will expire in 10 secs. It’s useful when implementing caching: we can place 30-60 minutes, as example, so as not to make data too stale if changes has been deployed
Also, just to mention, at first we check whether there is such key in the db, if not -> place it there, if yes -> return it. So, implementation of some kind of caching which will make response time faster.
+ in this implementation Redis is a separate entity which will make data persist even if main server crashes

![Alt text](ImageRepo/Key_value_Stores_third.png?raw=true)
