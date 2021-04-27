**Load Balancers**

Many Clients send requests to the Server => 1. make many servers to deal with it (<i>horizontally</i>) 2. Increase the power of current server (<i>vertically</i>). In many cases LB will be a reverse proxy. But not always: LB can be between Server and DB or at DNS layer (**``round-robin*`` **)

*Single domain name gets multiple IP addresses, when DNS query is made to get an IP address of that domain name, multiple IP addresses associated with that domain name will be returned in a load-balanced way. (Below) Same domain name has various endings of IP address due to the LB as round-robin.

![Alt text](ImageRepo/Load_Balancers_first.png?raw=true)

But how does it happen that Clients’ request come to various servers (balanced way)? => Load balancer.

Ex: Many clients’ requests go to LB at first and it distributes them to the servers

Result: improved throughput as servers aren’t overloaded and clients will have better latency.

**Note:** there are hardware load balancers and software ones. Latter one is more customizable and scalable => below software LB are used as base.

<ins><i>How does LB know about new server?</i></ins> People who are responsible for the system configure LB in such a way that they (LB & Server) register with each other in a moment of initialization. 

<ins><i>How does LB select servers to redirect traffic to?</i></ins> aka **Server selection strategy** 1. <ins>Random choice</ins> 2. <ins>Round-robin approach</ins> - LB redirects requests from top to bottom of the servers and so on 3. <ins>Waited Round-robin</ins> - main gist is the same as in point 2, but here we place a wait on a server then LB will redirect a little more on that server (for ex, if one of the servers is more powerful than the other) 4. <ins>Based on load</ins> - LB makes health checks of the servers to know how much traffic a server is handling/time to respond/amount of resources that server is using 5. <ins>IP address based</ins> - LB gets request from the client and hashes IP address of the client and depending on the hash number LB will redirect traffic accordingly. 6. <ins>Path-based</ins> - LB distributes requests according to the **path** of the request, i.e. on AlgoExpert requests related to code are redirect to one set of servers, requests related to payment to another set of servers etc.

Ex of IP based LB: if there is a **cache** in the system (you cache the results of requests in the servers), # then results of clients requests can be cached at the servers <br>
and requests of the specific clients can be redirected to the specific server in which response of that client has been cached

**Note:** in the system there can be multiple load balancers which use various server selection strategies

Ex: clients requests go to first and one load balancer which distributes them based on IP address to another load balancers (ex, two) which distribute based on round-robin strategy

**Note:** it’d better to place multiple load balancers at particular parts of the system to prevent overloading


(Below) When we hit server that listens to port 8081, requests will be redirected to load balancer named ‘nodejs-backend’. Load Balancer will reroute traffic to either of the two servers: localhost:3000 (listens to port 3000) and localhost:3001 (listens to port 3001) respectively. LB uses waited round-robin as first server has ‘waited’

![Alt text](ImageRepo/Load_Balancers_second.png?raw=true)
![Alt text](ImageRepo/Load_Balancers_third.png?raw=true)
![Alt text](ImageRepo/Load_Balancers_fourth.png?raw=true)
