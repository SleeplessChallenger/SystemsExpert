**Leader Election**

If we design system which has some <ins><i>Third-party services</i></ins>, then you don’t want them to interact with your <ins><i>DB</i></ins> as the latter one is a sensitive part. => Place system in the middle of those two machines above which will check DB and if required (for ex, check-up on a periodic basis) send request to that Third-party system. For example, to charge users.
<br>
Third-party service <- this system <-> DB

But having one system in the middle is a <ins><i>single point of failure</i></ins> => putting multiple ones with one as a <ins><i>leader</i></ins> is an option (so as not to repeat same requests from machines).<br>
So, leader will do all the work and other servers (here == systems) will sit by in case of something happening (so-called <ins><i>followers</i></ins>). And if something happens to the leader (like crash), then <ins><i>new leader</i></ins> will be elected. Difficult point here is **how to elect a leader** from multiple distributed machines that will share who the leader is? Even more, the stumbling point is how to make machines have consensus about who is the leader (**share the state** who the leader is).

To solve written above problem: **consensus algorithm** may be an option. 

**Consensus algorithms** - type of algorithms (i.e. Paxos, Raft) that allow multiple servers (nodes) in a cluster to reach consensus/agree on some single data value. In leader election this data value: who is the leader whilst in other cases something else can be.

In industry mostly people use third-party services/products that implement one of the consensus algorithms to achieve leader election so as not to do it themselves. <br>
<ins><i>Etcd & Zookeeper</i></ins> may allow you to implement leader election in an easy way. <br>
**Etcd** is a key-value store that is <ins><i>highly-available</i></ins> and <ins><i>strongly-consistent</i></ins>. How does Etcd achieve it? Due to leader election with consensus algorithm under the hood. So, Etcd can take care of servers from above and decide who is the leader & the followers

![Alt text](ImageRepo/Leader_Election_first.png?raw=true)

Ex: multiple servers communicate with Etcd (key-value store), and at any given moment we’ll have **one special key-value pair** in Etcd key-value store which will represent who the leader is: I.e. key: leader, value: name of the server/IP address of the servers

Example of implementation when one of server is leader. If it dies, one of the other servers takes his place.

![Alt text](ImageRepo/Leader_Election_second.png?raw=true)
