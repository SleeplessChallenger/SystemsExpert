**Specialized Storage Paradigms**


4 types here will be covered: **1. Blob store 2. Time Series DB 3. Graph DB 4. Spatial DB**

- Blob store (binary large object) - storage solution for blobs: arbitrary piece of unstructured data (video/image/text files). Used for storage of massive amounts of large unstructured data: Google Cloud Storage, S3 etc. Behave in way like **key-value store**, but they’re optimized for different cases. Ex: key-value store may not be optimized for such amount of data or be more optimized for latency rather than availability & durability. <br>
- Time Series DB - db specialized for storing time series data. When large amount of data relevant to time and some computations which require time series. <br>
- Graph DB - db that stores data following the graph data model. Good for data within which there are lots of <ins><i>relationships between data sets</i></ins> (SQL isn’t good here). Last point is at the core of graph db whilst in SQL it’s just implied. Ex: Neo4j. Social networks are used with such databases. <br>

**Cypher** - graph query language (similar to SQL for relational DBs)

- Spatial DB - databases that are optimized to store spatial data: geometric space (locations on a map). It comprises various concepts, one of which is **Quadtree**. They rely not on classic db indices, but on <ins><i>spatial indices</i></ins>. Quadtree is a structure that resembles ordinary Binary tree, but every node has  <ins><i>0 (leaf node) or 4 children nodes</i></ins>. It resembles some form of grid.

Red rectangle is our place (hotel/country etc). Small dots are locations on the map. Overall structure is divided into 4 rectangles and then another 4 rectangles and so on till the very cell (every rectangle can be either a leaf node - no further division - or represent 4 children nodes). 

**But:** you can change params and make leaf node if node has below 5 children and if more than 5 => continue dividing.

Green dots within a red rectangle is the result which will be returned to the client as we don’t want to throw thousands of matchings, but just first 10, for example.

![Alt text](ImageRepo/Specialized_Storage_Paradigms_first.png?raw=true)
![Alt text](ImageRepo/Specialized_Storage_Paradigms_second.png?raw=true)
![Alt text](ImageRepo/Specialized_Storage_Paradigms_third.png?raw=true)
