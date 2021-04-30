**Publish/Subscribe Pattern**

**Pub/Sub pattern** - paradigm that consists of 4 entities 

It somehow resembles **streaming**, but in streaming we have 1 client who is getting constantly flow from the server. But if we want to expand the system (have so-called large scale distributed system)? What if client loses connection/How to do network partition/What if server dies.
Also, we want to have a persistent storage so as if server crashes, data gets saved. But typical DB isn’t an option because what if we want some asynchronous operation when client makes request and goes further and respond to that request comes back afterwards. + uniting server and db to achieve above written goal isn’t the best decisions from business/design point of view
=> pub/sub pattern is an option<br>
```
1st entity: publisher
2nd entity: subscribers
3nd entity: topic
4th entity: message
```

![Alt text](ImageRepo/P_S_Pattern_first.png?raw=true)

Publishers can be considered as servers which publish data to topics (== channels). Subscribers listen to the particular topics rather than to the Publisher itself.
So, publisher and subscriber don’t know about each other and that topic is a some kind of intermediary between them.
That data from above can be named as message (that 4th entity) that subscribers will listen to. When message is published, it goes through channel to subscribers that are subscribed to that particular channel.

**Features of pub/sub system:** ```1. At-least-once delivery 2. Persistent storage 3. Ordering 4. replayability```

**Note:** message isn’t literally a message, it can be an operation (to execute a stock trade, for ex)<br>
Those messages will be stored within channels (topics) **in a persistent way (storage)** (if machine crashes -> data persists).<br>
Topics are like DB solution. Also, they **incorporate at-least-once delivery**: messages which are published to the channel are guaranteed to be delivered to all the subscribers at least once <br>
**How does it work more precisely?** When messages are sent to the channel, they have some index/id representing each of the subscribers so that when all the subscribers receive the message and send some response (ACK) back to the topic, that messages’ indices of every subscriber turns into ‘Delivered’ or something like that (i.e. Message1 id1: ‘Consumed by subscriber1’)

**At-least-once delivery vs once delivery**

When message is pushed out to the subscriber, subscriber may lose the connection in that moment to that topic and although has received a message, doesn’t send back any response (ACK). Hence, the topic may think that it has’t sent message (actually, the message itself will realize it) and when subscriber will reconnect, the topic will send it once more time (and it can repeat again). Introduces new topic => Idempotent

**Idempotent operation** - operation which has the same ultimate outcome regardless of how many times it has been performed. Ex: set the status of something to complete is idempotent. But ‘likes’ isn’t an idempotent operation as it increases the counter. 

=> That’s why at-least-once delivery should have idempotent operation (in most cases) (if multiple times same message was delivered and it increases something -> unlikely it’s good)

Another feature of pub/sub is **ordering**. Ordering of messages means that they’ll be pushed to subscribers in a way messages stay (like a Queue with LIFO).

Last one: **replayability**. So we can rewind/replay to the last/previous message

Actually, <ins><i>topic is a DB</i></ins>. Another way of creating system compared to ordinary Client - Server - Db one. That’s why having multiple topics is favorable as we can push stock prices to one topic and news alerts to another topic. And, for example, 3 topics can be a part of the same server cluster: 1st publisher sends stock prices to topic1, 2nd publisher sends crypto prices etc.

**Adding stuff on** pub/sub system is also an option. Ex, content based on filtering on the client side is also an option. For example, subscriber1 filters out all messages that contain tech stock prices whilst subscriber2 filters to receive only tech companies stock prices.

There are lots of popular pub/sub solutions like Apache Kafka or Google Cloud Pub/Sub. Using those systems will make your life easier: Google Cloud Pub/Sub tells you not to care about topics like sharding (topics will scale automatically) + they implement persistent storage. Also, end-to-end encryption is also implemented already in the system. Etc

![Alt text](ImageRepo/P_S_Pattern_second.png?raw=true)
