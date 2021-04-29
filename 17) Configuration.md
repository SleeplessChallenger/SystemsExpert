**Configuration**

**Configuration** - set of params/set of constants that the system is going to use, but instead of having them deeply intertwined in the code, they’re written in some seemingly isolated file. Generally, configuration files are done in **JSON** or **YAML**.

Two types of configuration: **static** and **dynamic**

**Static** - configuration that is bundled with the code. <br>
<ins><i>Pros</i></ins>: every change goes through code review process as you’re to **redeploy** (stop & start the server, for ex) the whole code => Safer <br>
<ins><i>Cons</i></ins>: slower

**Dynamic** - configuration that is completely separated from the application code. <br>
Can be changed at a moment => Faster. Also, dynamic configuration is more complex as it is to be backed by some DB which our system will query to see the current configuration. <br>
<ins><i>Pros</i></ins>: faster deployment of new features<br>
<ins><i>Cons</i></ins>: risk of unseen errors

![Alt text](ImageRepo/Configuration_first.png?raw=true)

![Alt text](ImageRepo/Configuration_second.png?raw=true)
