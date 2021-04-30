**MapReduce**

Appeared due to the fact that there is limit in <ins><i>vertical</i></ins> scale of the system and in some moment there is no other way, but to scale <ins><i>horizontally</i></ins>

**MapReduce** - framework that allows to process huge datasets spread across even thousands of machines very easily. So, 1. You have a large dataset 2. Via ‘map’ function you transform the dataset into intermediate values (<ins><i>key-value pairs</i></ins>) 3. In ‘shuffle’ step those pairs are reorganized so that same keys are routed to the same machine 4. Via ‘reduce’ function those shuffled pairs are put into some output.

![Alt text](ImageRepo/MR_first.png?raw=true)

**Notes:** 
1. We assume having some distributed file system: have some big dataset which chunks are split and spread across various machines (+ replicated). Our file system has some control and awareness over what is happening in the MapReduce process (so-called **central control plane**). 
Machines performing map and reduce are called **workers**. 
2. Data is generally located on various machines, so instead of moving data, we <ins><i>move our map function</i></ins> to the desired machine. 
3. <ins><i>Key-Value</i></ins> pair of intermediate data is very important: chunks of data processed in reduce phase come from various parts of the initial giant dataset and the one thing that may unite some chunks is key-value pair (more precisely, key). 
4. <ins><i>Fault-tolerance</i></ins> is indispensable. If there is network partition or something else, our central control plane will redo map/reduce operation. => map & reduce functions **must be idempotent**
Mostly what you care when dealing with MR: define map, reduce and what input, output (of map and reduce) will be.

**Canonical example of a MapReduce use case:** count the number of occurrences of words in a large text file. 

**Steps:**

![Alt text](ImageRepo/MR_Second.png?raw=true)

1. For example, map function will go through file (loop) and count the number of some word (letter) occurrences (those map functions work in parallel on various machines). 

Way of doing  functions (map/reduce)may vary: in map we can tally up occurrences at first or emit every occurrence of the word to somewhere. [Here use first case as example].

2. In shuffle stage unite those that have same keys to one reduce function (to one <ins><i>worker node</i></ins>)

3. In reduce it’ll count up words occurrences according to the keys and push them to some output file (see image)

Ex: count number of logs per service in a particular span of time in the system can be done via MapReduce

![Alt text](ImageRepo/MR_third.png?raw=true)
