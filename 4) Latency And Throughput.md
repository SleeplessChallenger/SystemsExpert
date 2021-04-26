**Latency And Throughput**

Latency - how long does it take for data to traverse a system (from one point to another in the system). Ex: Time for request to go from **Client** to **Server** and back

**Note:** example of Inter-Continental Round Trip is a packet sending from CA -> Netherlands -> CA;
Over Network is like a network request where call to API is made; from RAM is like reading a variable in a code

When you design system, ideally you want to minimize <i>latency</i>, but it depend on the system (so-called trade-offs)
Ex: lag in a video game is an example of **high latency** 


Throughput - amount of work that machine can handle in a given period of time. 
Ex: How much data can be transferred from one point in a system to another in a given amount of time. If we make request from Clients to one Server - how much requests can server handle in a given amount of time? (= how many bits can server handle/let through per second?)

**1Gbps** network is an example throughput (1 gigabyte per second)

Question: if increase throughput will it make any good? -> Not always as there will be bottlenecks eventually. Hence, multiple servers may be an answer.

Also, low latency doesn’t always mean that there will be no bottlenecks as system has, for example, low throughput, hence these 2 terms are not necessarily correlated. Don’t make assumptions about either of the term based on the other.

![Alt text](ImageRepo/Latency_Through.png?raw=true)
