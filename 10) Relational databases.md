**Relational databases**

**Relational database** - database that imposes tabular-like structure on the data stored in the database. The one who designs the system also designs the schema of the db -> tables.

**Non-relation database** - database that doesn’t impose any strict structure on the data.

SQL is a language to interact with relational databases. <ins><i>Powerful querying</i></ins> capabilities are the main reason why SQL is opted for.

SQL must use ACID transaction. **ACID transaction** that has 4 properties: atomicity, consistency, isolation, durability.

- <ins>Atomicity</ins>: either all the transactions succeed or fail. Transaction itself consists of multiple operations. For ex, when doing money transfer from one bank account to another: deducting from one account and increasing on another account (2 sub operations, where overall it’s known as unit). If not succeed -> rollback all the transaction<br>
- <ins>Consistency</ins>: every transaction in a db will conform to all rules in the db. Every future transaction in the database will take into account all the previous transactions. I.e **cannot be stale state** in the db: when one transaction doesn’t know that other has already performed == there will be no delay in the data state within the db<br>
- <ins>Isolation</ins>: execution of multiple **concurrent** transactions equals to execution of multiple **sequential** transactions<br>
- <ins>Durability</ins>: results of transaction in the db are permanent, i.e. data stored in db is stored on disk<br>


**Database index** - auxiliary data structure that will speed up the search within your database.
Pros: read operations faster Con: write operations slower. Must be created when the db is created

1. If you BEGIN TRANSACTION, then until you COMMIT and if you have done some changes to the db within this transaction, those changes can’t be seen if we query the table from somewhere else. **Example of atomicity**
2. If we BEGIN TRANSACTION within different sources and have done some changes to the db in one source, then making change within another source <ins>will make the query hang</ins> till that first TRANSACTION is committed. Then, if we COMMIT first TRANSACTION, then the second one will proceed out of the hang state and all the tweaks of the first TRANSACTION will be displayed. **Example of isolation**, TRANSACTIONs are done <ins>concurrently</ins>, but they’ll be executed <ins>sequentially</ins> + **Consistency** as every TRANSACTION knows the results of another one

<ins><i>Strong consistency</i></ins> is what is supposed in ACID whilst <ins><i>eventual consistency</i></ins> means that query may return result that is stale. DB data will reflect writes within a period of time like 10 sec or another.

![Alt text](ImageRepo/Relational_databases.png?raw=true)
