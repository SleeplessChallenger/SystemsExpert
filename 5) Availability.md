**Availability**

Other than Latency & Throughput, when designing a system one should ponder over availability. 

Availability - a % of systems uptime in a year.

In today’s market everything that is below 99% availability is bad, hence in the industry availability is measured in so-called **nines**. 99 % is a two nines availability, 99.99% is a four numbers availability.

**HA** - systems availability is 99.999% and higher

Service-level agreement (SLA): <ins>**a collection of agreements**</ins> between a service provider and customer on system’s availability amongst other things. Ex: ‘we guarantee you **this amount** of availability/uptime’.
SLO is not a synonym for SLA. SLA is made up of many SLOs

Service-level objective (SLO): **that** % of uptime guarantee is an SLO; I guarantee that you’ll have x number of errors when you use my service.

**Note:** high availability is very difficult to achieve, hence you need to make trade-offs.
For ex: Stripe has payment service which has to be HA, whilst other parts of the whole system like dashboard for businesses to monitor sales - not required HA.

<ins>**Ways to ensure the system not to fail:**</ins>

No single points of failure: if one place fails then whole system crashes.
How to eliminate them? With <i>**Redundancy**</i>
Act of multiplying the system certain parts

Ex of single point: many Clients -> Server -> DB. Here server is a single point, that’s why adding another server is an option + adding **load balancer** between Clients and servers to distribute them on the servers. But having only one LB is a single point => adding multiple of them

Stuff above is **Passive redundancy** 
If some part goes down (like one of the LB) then another ones will take the work till first is revamped
**Active redundancy** is when only particular amount of machines (from a group) handles operations and one of them fails (or the group of them) => other machines in the system know that something is broken and they reconfigure themselves.

2. Processes to handle outages swiftly.

![Alt text](ImageRepo/Availability.png?raw=true)
