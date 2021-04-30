**Client - Server**
[Browser] - [AlgoExpert]

Client is the machine which sends request to the Server. Server is the machine that responds to the Client with result.

**Note:** machine can have both roles simultaneously when being a server to the browser it can be a client to the database.

When you type www.Algoexpert.io: browser makes a **DNS** query to find what the **IP** address of the aforementioned site is and only after that it can speak to the site.
 
**DNS(domain name system):** special request that goes to a predetermined list of servers and requests the IP address of the desired site.  

**IP:** unique identifier of the machine.

After browser has received a response with **IP** address it sends an **HTTP** request to this **IP** address. Actually, it sends a bunch of bytes (characters) in packets with source address of a request (IP address of your browser/computer). 
Every machine that has distinct IP address obtains 16000 ports

Servers are machines which listen to requests from other machines on some **ports**. So, client has to specify which port it wants to communicate on. 
However, there are predefined ports which some protocols have:
HTTP: 80/HTTPS: 443/DNS: 53/Secure Shell: 22

After server has received a request, it understands that client wants to see HTML of the site.
Server returns the HTML of the site which browser renders.

**IP address** is address of the system in the Network.
**Port** is address of the service within the System.
So IP address + Port defines address of the particular service on the particular system

![Alt text](ImageRepo/Client_Server_first.png?raw=true)
