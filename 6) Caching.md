**Caching**

Caching is used to speed up a system (= improve <i>latency</i> of a system). Also, caching will store data in a new location, other than data itself, which it’ll be faster to retrieve data from compared to initial storage of data.

Client	  <->	Server	   <->	 Database

**Note:** cache can be at either of the levels or even between them (above)

Ex: 1. Client makes request to the Server which retrieves data from DB. **Cache** can be placed at Client or Server level if same request comes in the future.<br>
    2. Client again makes request, but now Server computes the desired response with, for example, algorithm with poor Complexity => cache may be an option.<br>
    3. Multiple clients make multiple <ins>**same**</ins> network requests to the servers => we can redirect requests to the cache instead of DB, or every server can have its own cache.

**Real example:** on AlgoExpert after user has visited questions list once and there has been load done, it’ll be cached for the future if user doesn’t close tab =><br>
questions are preloaded on the Client side <i>(if we exclude editing data)</i> instead of making network request to the server every time.
Next, if you run solution code (which was written by authors themselves) on AlgoExpert => from cache as well as there is no computation required. How it happens? HTTP Request from Client to Server (when user hits RUN), AlgoExpert server has this request (knows it), then hash that request and check this hash in cache which can be either on the server or detached from server (in ‘Redis’ as example). 


Client uploads post and we have cache on the server, but also there is DB where this post will be placed. If the client changes the post, how does cache get updated?

**Two cache systems:** <ins>write through cache & write back cache</ins>

First type: When some data appears, it’ll be written to both cache and DB. Weak point? Requires to visit DB every time

Second type: when some data appears, system will update **only** cache at first and go back to the client => cache is out of sync with DB. System will asynchronously update cache with DB (ex. every 5 secs/min etc or when cache gets full). Weak point: if system crashes before DB gets updated with cache => lost data.

**Stale cache** - cache with old data (that hasn’t been uploaded yet). Example: if YouTube had caches on the servers, then some comments may not be updated properly.
How to prevent it? Put cache outside the server somewhere else. For example, one cache between the servers.<br>
<i>But not all systems</i> require such technique and maybe some degree of staleness is Okay: YouTube views is not as important as comments.

That’s why if data is static/immutable or staleness is acceptable or single thing reads/writes data or able to get rid of stale data quickly in cache => caching in is great

**Cache eviction policy** - policy by which data gets evicted from the system. Ways: LRU (least-recently used), FIFO, LFU (least-frequently used).

+ We can use **CDN** (content delivery network) which acts like a cache for our system (see below for detailed explanation)

![Alt text](ImageRepo/Caching.png?raw=true)
