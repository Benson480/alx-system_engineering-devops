Web infrastructure design
0. Simple Web Stack

https://drive.google.com/file/d/18pHYmhRIkvDdSRB5ASnRyGGkDjYMaRWJ/view?usp=share_link

What is a server
Servers are physical machines (as hardwares), virtual machines or softwares (computer programs) that serve or provide functionality to other programs or devices called “clients”. The term server comes from queuing theory used in Kendall’s notation, where servers serve or process the clients requirements in the same way as a telephone operator, a cooker or a production machine process incoming orders, having in mind its capacity and service process time.

A computer can function as a server, and a server can be a computer, both of them being built up with hardware and software. However, the main difference between these two is the capacity and computer power servers have. In other words, servers are computers on steroids with faster processing capacity. They are usually stored in data centers racks (stacks of servers piled one on top of each other).

On the other hand, virtual servers function more like virtual machines, or virtual computers. These are a virtual representation of the physical servers, having their own operating system and applications (Posey, 2021).

(ejemplo de tipos de servers softwares) (tipos de servicios que ofrecen los servidores

What is the role of the domain name
The role of the domain name is to replace complex IP addresses numbers into easily understandable names so humans can remember and communicate them in a better way.

What type of DNS record www is in www.foobar.com
DNS record of www belongs to a subdomain of the www.foobar.com

What is the role of the web server
Web servers are what make Web hosting possible, that is, the possibility of renting a space on a server to store the files of our site.

The fundamental role of a Web Server

The main function of a Web server is to store the files of a site and broadcast them over the Internet so that they can be visited by users. Basically, a web server is a large computer that stores and transmits data via the network system called the Internet. When a user enters an Internet page, his browser communicates with the server sending and receiving data that determines what he sees on the screen. Therefore, we say that Web servers are to store and transmit data from a site as requested by a visitor’s browser.

What is the role of the application server
The application server is the intermediary between browser-based databases and back-end databases and legacy systems. In many uses, the application server combines or works with a web server (Hypertext Transfer Protocol) and is called a web application server.

What is the role of the database
The role of the database is to make the information gathered organized so it can be easily accessed, managed and updated. However, not all database management systems work the same, and the mechanisms they use to organize data can vary, ranging from relational database to object-oriented database, distributed database or cloud database. Next, some of its main differences:

Relational databases:

Are composed of a set of tables where data is organized into a predefined category. Each table has at least one data category in a column, and each row represents an instance of the categories defined in the columns. SQL (The Structured Query Language) is a popular example of a relational database.

Distributed database:

Distributed database system consists of portions of a database that can be heterogeneous or homogeneous distributed along multiple physical locations.

Cloud database:

Cloud database is a database built in a virtual environment, just as in a hybrid cloud, public cloud or private cloud. Scalability on demand, and hight availability are one of the benefits of having a cloud database.

NoSQL database:

Are useful for big data performance and large sets of distributed data, specially when the need of analyzing large sets of unstructured data stored across multiple virtual servers in the cloud.

Object-oriented database:

Another example is an object-oriented database which is organized around objects instead of actions (Hughes, 2019).

What is the server using to communicate with the computer of the user requesting the website
The server is using the HTTP (Hypertext Transfer Protocol), which enables the transfer of resource and data, such as HTML documents between the server and the client. In this data exchange the request is initiated by the client, which is done normally by web browser (it can also be done by an operating sistem or application) are called request and the server answers are called responses. Between the client and server data exchange we can find numerous entintes, collectively called proxies, performing different operations such as gateways or caches.

From the client side (the browser) is the one who always initiates the request to the server of the data such as the HTML and CSS files, never the other way around. Once the request is received by the server, it serves the documents as requested by the client, so it can finally present the Web Page. (Mozzila.org)

Issues with the simple web infrastructure
One of the issues of having a simple web infrastructure, has to do with the SPOF (Single Point of Failure) where if component of the system fails, there is no backup that can support the continuity of the functionality of the system, bringing the whole system to a collapse by being unable to operate.
Also, whenever some structure or node in the system needs to be repaired, the whole system has to be shut down, while the maintenance is done. Then, client requests cannot be attended during this period of time.
Overload of traffic can be a risk to the server capacity. This, because there is no possibility to scale the service with additional servers as backup. Leading to a possible breakdown of the web page and client requests, as traffic surpasess servers capacity.
1. Distributed Web Infrastructure

https://drive.google.com/file/d/1UHa5alIu3CiikDtPbuDmpK7cTe0sflaV/view?usp=share_link

For additional element, why you are adding it?

The new configuration is composed of two master-servers and one slave-servers. As the master-servers are going to be working based on a Active-Active set up, their configuration must be identical, therefore we need to add every additional element as the simple web infrastructure we had in the previous point. The load is going to be managed through a load-balancer, which distributes the queries according to a Robin-Round algorithm. Finally an additional server will be needed to serve a replica or slave server, helping to unload the masters servers reading queries.

What distribution algorithm your load balancer is configured with and how it works

Our load-balancer is using a Round Robin algorithm distribution. Meaning the queries requested are distributed to every server sequentially one after another. And after sending the request to the last server, the algorithm startarts from the first server. This will bring on average and approximately, to a server load distribution of 50% on each of the two servers configuration.

Is your load-balancer enabling an Active-Active or Active-Passive setup, explain the difference between both

Our load-balancer is enabling an Active-Active set up.

The Active-Active cluster is typically made up of at least two nodes, both activaley running the same type of services at the same time. Their purpose is to achieve load balancing by distributing tasks to different servers in order to prevent overload. As there are more than one servers (nodes) available to severe, the service time and process throughput can have improvements.


Image source: (Lutkevich, 2020)
On the other hand the Active-Passive setup, also made up of at least two nodes (servers), however not all nodes are going to be active simultaneously. In this configuration, while one node is active, the other nodes (failover servers) are passively waiting to be active as backup in case the primary server (the one being in use actively) is disconnected or unable to serve. Under this configuration, and as in the Active-Active set up, it is important that primary and failover nodes have the exact server configuration, so clients won’t be able to tell the difference when the failover server takes over the operation (Villanueva, 2017).


Image source: (Lutkevich, 2020)
How a database Primary-Replica (Master-Slave) cluster works

A database Primary-Replica (Master-Replica) is a mechanism which enables data of one database server (the master) to be replicated or to be copied to one or more computers or database servers (the slaves), in order all users share the same level of information. This process leads to a distributed database in which users can quickly access data without interfering with each other.

The database replication process can either be synchronous or asynchronous. In the first one, the replication process is done from the client server to the model server and then replicated to all the replica servers before the client is notified about the data replication. This method of replication may take longer to verify, however all data was copied before proceeding.

As in the asynchronous replication process, replication is done by sending data from the client to the model server, followed by a confirmation order to the client, who finally gives permission of copying to the replicas at an unspecified or monitored pace (Lutkevich, 2020)

What is the difference between the primary node and the replica node in regard to the application.

One of the main differences between the primary node and the replica node, regarding the application, is that the primary database is regarded as the authoritative source, while the replica database is synchronized to it. The primary node serves as the keeper of information, here the “real” data is kept, then writing only happens here. On the other hand, reading only occurs in the replica or slave node. This architecture purpose is due to safeguard site reliability. In case a site receives a lot of traffic, a replica node prevents overloading of the master node with reading and writing requests. This eases the load of the entire system preventing it to collapse (Theodorus, 2020).

Issues with the distributed web infrastructure
2. Secured and monitored web infrastructure

https://drive.google.com/file/d/1tcX0S5s2RjUglZOx1WQ1TwPmytAspub-/view?usp=share_link

For every additional element, why you are adding it

3 Firewalls: The first Firewall checks the rules after receiving the requests and could deny following requests. The second firewall is working in the server to prevent someone hacking depending of the requests, and the third firewall acts as a circuit-level firewalls, inspect the transaction of the information.
SSL certificate: 1 SSL certificate: is added to secure https protocols and encrypt communication. Then, the ‘plain text’ won’t be easy accessed or viewed by a third person, making the protocol communication and data transfer form the browser and web server more secure (Instant SSL, 2021)
What are firewalls for

Firewalls is a network security device that monitors network traffic, it can be understood as a division or “wall” between a private network and public network which limits and blocks network traffic based on a set of security rules in the hardware or software by analyzing data packets that request entry to the network. Additionally, firewalls are used to allow remote access to a private network through secure authentication (Beal, 1996)

Why is the traffic served over HTTPS

HTTPS stands for HyperText Transfer Protocol Secure, and the traffic is served in order to bring protection by using the secure port 443, which encrypts outgoing information. Then it is more difficult to spy or get access to the site’s information.

What monitoring is used for

Monitoring is practice used for quality control. As Peter Ducker said, “What can’t be measured, it can’t be improved”. Then, monitoring not only helps to make sure to maintain high quality levels, keeping the established standards and consistency, but also to help in the continuous improvement of the resources performance.

The way data monitoring is performed, relies on checking new data against predefined rules and metrics. If data quality anomalies are detected, an alert is sent in order to give information about the metrics and rules violation, so data can be checked (Informatica, 2021).

3 monitoring clients: 2 monitoring deployed in each master-server, and one monitoring client for the load balancer. This will help understand the metrics of the performance of the resources according to the users requests. The information gathered will help us improve users’ experience and make decisions on the future whether to scale up the web infrastructure system.

How the monitoring tool is collecting data

IT monitoring is composed of three parts: 1) Fundation; 2) Software, and 3) Interpretation in order to function.

Foundation: Are related to the infrastructure at its lowest layer of the software stack. This includes physical and virtual devices, such as servers, CPUs and VMs.
Software: The software is the monitoring section which analyzes what is happening in the devices (physical or virtual machines) in terms of CPU usage, load, memory, and running count.
Interpretation: Here is where collected data is turned into metrics and are presented through graphs or data charts (mostly on GUI dashboard). This is often integrated with tools of data visualization to help better understand and do data analytics of performance (Gillis, 2020).
Explain what to do if you want to monitor your web server QPS

Queries per second is a measure of the rate of traffic going in a particular server serving a Web domain. It is an important metric to monitor, because it can help you decide whether to scale the server in order to cope with the demand of usage, and resource requirement so the web page won’t collapse in the future with overload server request.

Issues with the secured and monitored web infrastructure
3. Scale up

https://drive.google.com/file/d/18JKYD4UUKumFNNo_SJi91Me17dCq9CKo/view?usp=share_link

Authors:

Benson mwangi <bensonmwwangi102@gmail.com>
Stephanie Iman
