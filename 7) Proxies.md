**Proxies**

Proxy is usually referred as forward proxy

**Forward proxy** is a server that sits between client(s) and server(s). It acts on behalf of the client(s).
When client makes request to the server, this request will go at first to the proxy which will forward the request to the Server. Hence, response from the server will also go through the proxy.
<ins><i>Proxy will hide the identity of the client</i></ins> as source address of the client will be replaced by the proxy’s source address. VPNs work in such way

If there is **Reverse Proxy** between Client and Server, when Client makes request, it’ll go to that R. Proxy at first [**Client doesn’t know that there is some R. Proxy between him and Server**] and then to Server. Whilst response from the Server will also go through R. Proxy.
When you type some site, like www.AlgoExpert.io and the site has reverse proxy, then your browser’s DNS query will go to R. Proxy which reroutes request to the Server which returns response. But the IP address returned to the Client will be the R. Proxy’s one, not Server’s one.

Use of Reverse Proxy: 1. Filtering out requests 2. Logging 3. Caching (ex. HTML Pages) so not to bother the server 4. as Load balancer - reverse proxy will decide to which server send the request


**********************
Proxy vs Reverse Proxy

Proxy:
```
Client1	->	
Client2	->	Proxy -> Server
Client3 ->
```
Proxy hides identity of the client for the server

Client makes request, request goes through proxy and proxy will make request to the server so as
server doesn't know who the client is

Benefits: 1) anonymity 2) caching 3) blocking unwanted sites 4) GeoFencing

Reverse Proxy:
```
Client -> Reverse Proxy -> Server1
			                  -> Server2
		                    -> Server3
```
Proxy hides identity of the server for the client

Benefits: 1) load balancing 2) caching - keeping content that doesn't really change 3) isolating internal traffic 4) logging 5) canary deployment - some part of the clients will receive a different kind of response (API is the same, but content differs)

Client inputs some into search bar -> reverse proxy will pick between available servers and opt for the best one (or free one)
***********************



Below you can see that due to ‘Nginx’ we can hide our localhost by ‘nodejs-backend’ name

![Alt text](ImageRepo/Proxies_first.png?raw=true)
![Alt text](ImageRepo/Proxies_second.png?raw=true)
![Alt text](ImageRepo/Proxies_third.png?raw=true)
