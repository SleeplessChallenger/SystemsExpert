**Polling And Streaming**

**Socket** - a kind of file that acts like a stream. Processes can read and write to sockets and communicate in this manner. Most of the time the sockets are fronts for TCP connection.

What if you design a system when clients will need data that is updating regularly? (Ex: weather app or chat app) <br>
=> **Polling and streaming come into play**.

**Idea behind polling:** client issues a request for data that he wants <ins><i>on a recurring basis</i></ins> following a set interval. For ex, client makes a request every 10 seconds.
Limitations: no instantaneous thing which is required in messengers. Of course, we can decrease the interval to 1/0.5 secs, but it puts a lot of load on a server. <br>
**Streaming** is an option!

**Idea behind streaming:** client will have a long-lived connection with the server through socket (file on your PC that your PC can write to and read from to communicate with another computer in a long-lived connection way. So, it enables two computers to interact with each other without need to constantly reconnect. Also can think of a socket as a portal into another computer which you can communicate through). Streaming allows to have a continuous stream of data.
<br>
<ins><i>Client is streaming data from server</i></ins>

![Alt text](ImageRepo/Polling_Streaming_first.png?raw=true)

Difference from polling is that in streaming client doesn’t request data from server, but just listens to the server if the latter wants to send data. Servers will **push** (phrase) data to clients.

**Note:** Neither of those two is better than the counterpart, it all depends on the system.

![Alt text](ImageRepo/Polling_Streaming_second.png?raw=true)
