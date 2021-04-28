**Peer-To-Peer Networks**

If we design a system which will transfer some amount data (i.e. 5 GB files) to thousands of machines multiple times in a day. How to speed up the process and eliminate bottleneck related to only one machine being responsible for all the work? 

1. **Increase amount** of machines that will have the desired data and they’ll give out the file in a distributed manner: those thousands of machines will ask for data from various machines => some boost is seen. But in this methods it means that those 5 GB files are **to be replicated** on all the additionally put machines

2. **Sharding** - some of the files of the overall data will live in one machine, another part in another and so on. But if we want to transfer one of the files (from all the data chunk), then those thousands machines will go to the same machine (server) that possesses that part of the overall data => once again bottleneck

=> **Peer-To-Peer network** is an option. From now on those thousands of machines will be called **peers**. <br> 
<ins><i>General gist</i></ins> of the design: divide desired file into very small parts and send those parts to all the peers. Then let those peers communicate with each other to grab the missing parts that they all need to create the final file and let them build the total file. <br>
Ex: 5 GB file / 1000 = **1000** * 5 MB files. 1 <ins>1 MB</ins> file to each machine (out of thousand) => with overall speed of 5 Gbps, the above task will take 1 second. Then, for every machine it’ll take 1 second to garner all the left files from other machines. So, if fine-tuned right, every machine will talk to another machine whilst other machines do the same and so on.

**Steps in a peer-to-peer network:**

- single step - transfer of 5 MB. It takes 0.001s to transfer 5 MB with current speed (5 Gbps)

1. first machine throughout all the thousand ones receive first part from main machine

2. That first machine sends its part to one of the peers whilst main machine sends another 5 MB chunk to another machine (peer) of the thousand peers. 
And the process goes on.

![Alt text](ImageRepo/Peer_To_Peer_Networks_first.png?raw=true)

But in real system we don’t want to be the selection of peers random => **Peer discovery/Peer selection** - peers know what peers to communicate with next. But how to do it? a) have DB (known as **Tracker**) which will know which peer to talk to next (when peers want to communicate with another peer, they at first communicate to that Tracker and it tells them which one to talk to next) <br>
b) **Gossip/Epidemic protocol** - peers themselves talk to each other to say what last peer they talked to and what part it has (without central DB): i.e. peers have mappings which say what peers possess which part of the file (I.e. IP address of the peer is mapped to chunk integer). Such kind of mapping is known as **distributed hash table (DHT)**

![Alt text](ImageRepo/Peer_To_Peer_Networks_second.png?raw=true)
