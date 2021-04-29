**Logging And Monitoring**

**Logging** - process of collecting data about some events in the system. Ex: user bought product, but doesn’t have access to it -> look at the logs of the particular user.

In other words, when we speak about logging, it does mean **having system/service** that will collect all the logs and store them in some DB so that we can go further to it and look at the logs to debug issues.

But how to gather them? Use, for example, special library to put log statements in the code to log important information and special format like <ins>syslog</ins> or <ins>json</ins>. So, the system will collect those formats and store in DB. (i.e on Google Stack Driver)

**Monitoring** - thing/tool to enable visibility of the system’s health. I.e. are there any error/high latency/how well authentication service work/how many sales you make per day.

How to create metrics for monitoring? Use pre-build tool (or build your own) to scrape your logs and create metrics out of them.

**Note:** if you want particulate metric -> you’re to have it in your log. Like latency: log every request latency in the system. <br>
**But** such method is not the best option as if you change your logs, then monitoring system can break down. <br>
<i>Use Time-Series DB!</i> (I.e. InfluxDB, Prometheus DB)

Hence, your servers will periodically send metrics to that DB. Then, you can query that DB.
Also, you can use tools to create graphs (image) out of Time-Series DB.

![Alt text](ImageRepo/Logging_Monitoring_first.png?raw=true)

**Alerting** - notification when some metric passes error threshold.

Ex: monitoring system can be hooked up into Slack so when some error spikes, alerting will be sent to Slack chat.

![Alt text](ImageRepo/Logging_Monitoring_second.png?raw=true)
