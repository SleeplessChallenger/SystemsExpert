**Hashing**

**Hashing function** - type of function that takes in specific data (either string or identifier) and outputs a number.<br>
<ins><i>Decreasing collisions -> increasing uniformity</i></ins>

***********
Good hash function should: 1)be fast 2)distribute keys uniformly 3)be deterministic (exact output every with certain input)

To deal with collisions we can use: separate chaining & linear probing

First method involves 'at each index in array 
store values using more sophisticated data structure 
i.e. array (nested one) or linked list'

Second method:when collision is found we search through 
array to find the next empty slot, but it has limit of array length
**************

Clients -> one load balancer -> servers

If we use **caching** in our system, then request from particular client should be redirected to particular server where response is cached => basic round-robin is unacceptable (when requests will be redirected to either of the servers in top-bottom manner). Use hashing!

**Example:** hash the names of the clients -> get number

1. Hash the name of the client and mod (%) the number (hashed result) by the number of servers => every client is associated with particular server to which all the requests from the particular client will be rerouted

**Uniformity** - even distribution of hashing function results

But there is problem with above mentioned design: if one server dies or we add new server? Then, if we mod again our clients we’ll receive completely different results. Here **consistent hashing** and **rendezvous hashing (highest random weight)** appear

<ins>Consistent hashing</ins>
1. Circle which depicts numbers, like 360
2. Put servers on the circle by applying hashing function on them. Ex, hash names of the servers and based on that values put them on the circle
3. Position clients on the same circle by the same manner as servers in point 2.
4. Go in clockwise/counter clockwise direction and the first server that will be encountered after the particular client => the server which load balancer will reroute the client (request) to.
5. If server dies, then client will just encounter next, after dead one, server. Same with adding new server. 
6. In result we’ll have better **cache hits** rate

Due to such technique there are fewer parts affected in the system. Consistency between hashes and target buckets.

**How to improve above structure?**  Pass every server via multiple hashing functions and results of them put on the circle => increase presence of every server on the circle => better uniformity

+ if one of the servers is more powerful => put it through more hashing functions compared to others => put results on the circle => greater amount of that server on the circle

<ins>Rendezvous hashing</ins>

1. Hash function will define highest ranking servers (from best rank to worst) for every user by some obscure logic.<br>

In background hash function calculates scores for every server/destination bucket -> pick the highest one -> your value (here username) will be associated with that highest one
 
2. Imagine, server5 dies. user1 has as highest ranking server server2, user2 has as highest ranking server server5. With former user nothing happens, with latter - it’ll take the next in priority server (look at photo below left one)

![Alt text](ImageRepo/Hashing_first.png?raw=true)
![Alt text](ImageRepo/Hashing_second.png?raw=true)
![Alt text](ImageRepo/Hashing_third.png?raw=true)
