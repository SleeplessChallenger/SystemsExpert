**Rate Limiting**

**Rate limiting** - thresholds on certain operations passed which these operations will return errors; limiting amount of operations that can be performed in a given amount of time

Ex: Client <-> Server <-> Database. Client can issue only 2 request in 10 seconds, if more -> server returns error

Rate limiting is essential as helps to prevent **DoS attack** (denial of service attack). It means that malicious user floods the system with a great amount of requests (traffic) to bring the system down.

It’s possible to **rate limit** based on various things (for ex, users). We can look at headers in request (i.e. authentication credentials) to identify the user and rate limit him to, for ex, 3 operations per minute. Also, limiting on region , IP address, whole our system (if system gets greater amount of requests than threshold => return errors).

However, <ins><i>rate limiting isn’t a silver bullet</i></ins> as it can fight back simple DoS attacks, but **DDoS** (distributed denial of service attack) will circumvent it as requests go from various machines.

**Note:** 1) First option is to have a rigorous load balancer. load balancer is essential as it’ll send requests of the user to the same server that caches the time of the previous request, otherwise the whole rate limiting is useless. 2) Another option is having a separate DB (although, Load balancer may still be in place). That’s why in distributed system rate limiting is handled not in memory of the service, but in a separated db which all servers will speak to (i.e. by Redis).

Ex: multiple clients make requests which will likely go through reverse proxy or straight to the server. Either of them will go, at first, to Redis to check about the rate limiting and if okay -> go to the db, for example. If not -> return error.

**Note:** rate limiting can be executed **in tiers**. Real Example: on AlgoExpert users can click on ‘Run code’ button every 0.5 seconds, but in 10 seconds they cannot do it more than 3 times, whilst in1 minute more than 10 time will return errors.

![Alt text](ImageRepo/Rate_Limiting.png?raw=true)
