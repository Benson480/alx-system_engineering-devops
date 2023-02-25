0x09. Web infrastructure design
Concepts
DNS

Monitoring

Web Server

Network basics

Load balancer

Server

What is a database

What’s the difference between a web server and an app server?

DNS record types

Single point of failure

How to avoid downtime when deploying new code

High availability cluster (active-active/active-passive)

What is HTTPS

What is a firewall

Application server vs web server

Tasks
0. Simple web stack
Description
This is a simple web infrastructure that hosts a website that is reachable via www.foobar.com. There are no firewalls or SSL certificates for protecting the server's network. Each component (database, application server) has to share the resources (CPU, RAM, and SSD) provided by the server.

Specifics About This Infrastructure
What a server is.
A server is a computer hardware or software that provides services to other computers, which are usually referred to as clients.

The role of the domain name.
To provide a human-friendly alias for an IP Address. For example, the domain name www.wikipedia.org is easier to recognize and remember than 91.198.174.192. The IP address and domain name alias is mapped in the Domain Name System (DNS)

The type of DNS record www is in www.foobar.com.
www.foobar.com uses an A record. This can be checked by running dig www.foobar.com.
Note: the results might be different but for the infrastructure in this design, an A record is used.
Address Mapping record (A Record)—also known as a DNS host record, stores a hostname and its corresponding IPv4 address.

The role of the web server.
The web server is a software/hardware that accepts requests via HTTP or secure HTTP (HTTPS) and responds with the content of the requested resource or an error messsage.

The role of the application server.
To install, operate and host applications and associated services for end users, IT services and organizations and facilitates the hosting and delivery of high-end consumer or business applications

The role of the database.
To maintain a collection of organized information that can easily be accessed, managed and updated

What the server uses to communicate with the client (computer of the user requesting the website).
Communication between the client and the server occurs over the internet network through the TCP/IP protocol suite.

Issues With This Infrastructure
There are multiple SPOF (Single Point Of Failure) in this infrastructure.
For example, if the MySQL database server is down, the entire site would be down.

Downtime when maintenance needed.
When we need to run some maintenance checks on any component, they have to be put down or the server has to be turned off. Since there's only one server, the website would be experiencing a downtime.

Cannot scale if there's too much incoming traffic.
It would be hard to scale this infrastructure becauses one server contains the required components. The server can quickly run out of resources or slow down when it starts receiving a lot of requests.

1: Distributed Web Infrastructure
Description
This is a distributed web infrastructure that atttempts to reduce the traffic to the primary server by distributing some of the load to a replica server with the aid of a server responsible for balancing the load between the two servers (primary and replica).

Specifics About This Infrastructure
The distribution algorithm the load balancer is configured with and how it works.
The HAProxy load balancer is configured with the Round Robin distribution algorithm. This algorithm works by using each server behind the load balancer in turns, according to their weights. It’s also probably the smoothest and most fair algorithm as the servers’ processing time stays equally distributed. As a dynamic algorithm, Round Robin allows server weights to be adjusted on the go.
The setup enabled by the load-balancer.
The HAProxy load-balancer is enabling an Active-Passive setup rather than an Active-Active setup. In an Active-Active setup, the load balancer distributes workloads across all nodes in order to prevent any single node from getting overloaded. Because there are more nodes available to serve, there will also be a marked improvement in throughput and response times. On the other hand, in an Active-Passive setup, not all nodes are going to be active (capable of receiving workloads at all times). In the case of two nodes, for example, if the first node is already active, the second node must be passive or on standby. The second or the next passive node can become an active node if the preceding node is inactive.
How a database Primary-Replica (Master-Slave) cluster works.
A Primary-Replica setup configures one server to act as the Primary server and the other server to act as a Replica of the Primary server. However, the Primary server is capable of performing read/write requests whilst the Replica server is only capable of performing read requests. Data is synchronized between the Primary and Replica servers whenever the Primary server executes a write operation.
The difference between the Primary node and the Replica node in regard to the application.
The Primary node is responsible for all the write operations the site needs whilst the Replica node is capable of processing read operations, which decreases the read traffic to the Primary node.
Issues With This Infrastructure
There are multiple SPOF (Single Point Of Failure).
For example, if the Primary MySQL database server is down, the entire site would be unable to make changes to the site (including adding or removing users). The server containing the load balancer and the application server connecting to the primary database server are also SPOFs.
Security issues.
The data transmitted over the network isn't encrypted using an SSL certificate so hackers can spy on the network. There is no way of blocking unauthorized IPs since there's no firewall installed on any server.
No monitoring.
We have no way of knowing the status of each server since they're not being monitored.
2: Secured and Monitored Web Infrastructure
Description
This is a 3-server web infrastructure that is secured, monitored, and serves encrypted traffic.

Specifics About This Infrastructure
The purpose of the firewalls.
The firewalls are for protecting the network (web servers, anyway) from unwanted and unauthorized users by acting as an intermediary between the internal network and the external network and blocking the incoming traffic matching the aforementioned criteria.
The purpose of the SSL certificate.
The SSL certificate is for encrypting the traffic between the web servers and the external network to prevent man-in-the-middle attacks (MITM) and network sniffers from sniffing the traffic which could expose valuable information. The SSL certs ensure privacy, integrity, and identification.
The purpose of the monitoring clients.
The monitoring clients are for monitoring the servers and the external network. They analyse the performance and operations of the servers, measure the overall health, and alert the administrators if the servers are not performing as expected. The monitoring tool observes the servers and provides key metrics about the servers' operations to the administrators. It automatically tests the accessibility of the servers, measures response time, and alerts for errors such as corrupt/missing files, security vulnerabilities/violations, and many other issues.
Issues With This Infrastructure
Terminating SSL at the load balancer level would leave the traffic between the load balancer and the web servers unencrypted.
Having one MySQL server is an issue because it is not scalable and can act as a single point of failure for the web infrastructure.
Having servers with all the same components would make the components contend for resources on the server like CPU, Memory, I/O, etc., which can lead to poor performance and also make it difficult to locate the source of the problem. A setup such as this is not easily scalable.
3: Scaled Up Web Infrastructure
Description
This web infrastructure is a scaled up version of the infrastructure described Secured and Monitored Web Infrastructure. In this version, all SPOFs have been removed and each of the major components (web server, application server, and database servers) have been moved to separate GNU/Linux servers. The SSL protection isn't terminated at the load-balancer and each server's network is protected with a firewall and they're also monitored.

Specifics About This Infrastructure
The addition of a firewall between each server.
This protects each server from unwanted and unauthorized users rather than protecting a single server.
Issues With This Infrastructure
High maintenance costs.
Moving each of the major components to its own server, means that more servers would have to be bought and the company's electricity bill would rise along with the introduction of new servers. Some of the company's funds would have to be used to buy the servers and pay for the electricity consumption needed to keep the servers (including the new and old ones) running.

Concepts notes used

			0x09-web_infrastructure_design
Web infrastructure design refers to the process of designing the physical and logical components that make up a web application or website. This includes everything from the hardware and software systems to the network architecture and security measures.
In designing web infrastructure, several key considerations need to be taken into account. These may include factors such as scalability, availability, performance, security, and cost-effectiveness.
Scalability involves designing the system to handle increasing amounts of traffic and data as the website grows. Availability involves ensuring that the website is always accessible to users. Performance involves optimizing the system for speed and responsiveness. Security involves protecting the system from attacks and unauthorized access. Cost-effectiveness involves ensuring that the infrastructure design is efficient and cost-effective.
The specific design of web infrastructure will vary depending on the needs of the particular website or application, and may involve a combination of physical and virtual components such as servers, databases, load balancers, firewalls, and content delivery networks (CDNs).
Designing a web infrastructure requires careful planning and consideration of various factors to ensure that it meets the needs of the application and its users. Here are some general steps to consider when designing a web infrastructure:
Determine the needs of the application: Before starting the design process, it is important to understand the requirements of the application. This includes factors such as the number of users, the amount of traffic expected, the types of data being processed, and the level of security needed.
Choose a hosting provider: The next step is to select a hosting provider that can meet the needs of the application. Factors to consider include the type of hosting (shared, dedicated, or cloud), the level of support provided, the scalability options, and the cost.
Select a web server: Once a hosting provider has been chosen, the next step is to select a web server. Popular web servers include Apache, NGINX, and Microsoft IIS. Factors to consider when selecting a web server include performance, security, and ease of use.
Choose a database: Depending on the needs of the application, a database may be required to store and retrieve data. Popular databases include MySQL, PostgreSQL, and Microsoft SQL Server. Factors to consider when selecting a database include scalability, security, and ease of use.
Configure the server: After selecting the web server and database, the next step is to configure the server to meet the needs of the application. This includes setting up the necessary software and configuring security settings.
Implement caching: Caching can significantly improve the performance of a web application by reducing the amount of time required to retrieve data. Popular caching solutions include Memcached and Redis.
Implement load balancing: Load balancing distributes traffic across multiple servers to ensure that the application can handle a high volume of traffic. Popular load balancing solutions include HAProxy and NGINX.
Monitor performance: Finally, it is important to monitor the performance of the web infrastructure to identify any issues and ensure that it is performing optimally. This can be done using tools such as Nagios, Zabbix, or Prometheus.
Overall, designing a web infrastructure requires careful planning and consideration of various factors to ensure that it meets the needs of the application and its users.
CONCEPTS
1.	DNS stands for Domain Name System. It is a system used to translate human-readable domain names, such as www.example.com, into IP addresses, such as 192.0.2.1, which are required for communication between devices on the internet. When a user types a domain name into a web browser, the browser sends a request to a DNS resolver, which is typically operated by the user's Internet Service Provider (ISP) or a third-party DNS provider. The DNS resolver then looks up the IP address associated with the domain name in a hierarchical and distributed database called the DNS hierarchy. This database contains records that map domain names to IP addresses, and the records are maintained by various organizations, including domain name registrars, web hosting companies, and DNS service providers.

Once the DNS resolver has obtained the IP address associated with the domain name, it returns that information to the user's web browser, which can then use that IP address to establish a connection with the web server hosting the website associated with that domain name. DNS is a critical component of the internet infrastructure, as it enables users to access websites and other online resources using human-readable domain names rather than numerical IP addresses.
2.	DNS uses various types of records to map domain names to IP addresses, as well as to store other information about domain names. The following are some of the most common types of DNS records and their functions:
•	A Record: An A Also known as Address record maps a domain name to an IPv4 address. For example, the A record for www.example.com maps the domain name to the IP address 192.0.2.1.
•	AAAA Record: An AAAA record maps a domain name to an IPv6 address. For example, the AAAA record for www.example.com maps the domain name to the IPv6 address 2001:db8::1.
•	CNAME Record: A CNAME Also known as Canonical Name record creates an alias for a domain name. For example, the CNAME record for www.example.com might point to the domain name webserver.example.com. This allows users to access the website using either domain name.
•	MX Record: An MX Also known as Mail Exchange record specifies the mail server responsible for accepting email messages for a domain. For example, the MX record for example.com might specify the mail server mail.example.com.
•	TXT Record: A TXT Also known text record allows arbitrary text to be added to a DNS record. This is often used for implementing Sender Policy Framework (SPF) records, which specify which servers are authorized to send email on behalf of a domain.
•	NS Record: An NS Also known as Name Server record specifies the authoritative DNS servers for a domain. For example, the NS record for example.com might specify the DNS servers ns1.example.com and ns2.example.com.
•	SOA Record: An SOA Also known as Start of Authority record specifies the primary DNS server for a zone and contains administrative information about the zone, such as the email address of the domain administrator.
•	SRV Record: An SRV Also known as Service record specifies the location of a service within a domain. For example, an SRV record might specify the location of a VOIP server within a domain.
•	PTR Record: A PTR Also known as Pointer record maps an IP address to a hostname. For example, the PTR record for 192.0.2.1 might map the IP address to the hostname webserver.example.com. This is often used in reverse DNS lookups to determine the hostname associated with an IP address.
The root domain and sub domain – differences
A root domain is the top-level domain (TLD) of a website, such as ".com", ".org", or ".net". It is the primary domain that represents the website and is typically used to denote the purpose or type of the website. For example, ".com" is commonly used for commercial websites, while ".org" is often used for non-profit organizations.
A subdomain is a domain that is part of a larger domain, located to the left of the root domain. It is created by adding a prefix to the root domain name, such as "blog" or "store". For example, "blog.example.com" is a subdomain of "example.com". Subdomains are often used to separate different sections of a website or to create distinct web applications or services.
In summary, the main differences between a root domain and subdomain are that a root domain is the primary domain of a website, while a subdomain is a domain that is part of a larger domain and can be used to separate different sections of a website or create distinct web applications or services.
What Is Round Robin DNS?
Round Robin DNS is a method of load balancing a cluster of servers using the Domain Name System (DNS). In this method, multiple IP addresses are assigned to a single domain name, and DNS servers return a different IP address for each request in a cyclical or round-robin fashion.
When a client sends a request to the domain name, the DNS server responds with the first IP address in the list. For the next request, the DNS server responds with the next IP address, and so on. This distributes the traffic evenly among the servers in the cluster, allowing for increased scalability and redundancy.
Round Robin DNS is a simple and cost-effective way to balance traffic among multiple servers, but it has some limitations. It doesn't provide any failover capabilities, and it doesn't take into account server capacity or availability. It's also possible for some clients to receive slower responses if they happen to be directed to a busy or underperforming server. For these reasons, more advanced load-balancing techniques, such as dynamic DNS, may be preferable in certain situations.

Web stack monitoring
Web stack monitoring refers to the practice of monitoring and analyzing the performance and health of the various layers of a web application stack. A web application stack is composed of multiple layers, including the client-side layer (web browser), the server-side layer (web server, application server, database server), and the networking layer (load balancer, firewall).
Web stack monitoring involves collecting and analyzing data from each layer of the stack to gain insights into the performance and behavior of the web application. This data can include metrics such as response time, error rates, throughput, and resource utilization.
By monitoring the web stack, organizations can identify potential performance issues, detect security threats, and troubleshoot problems that may arise in the application. This helps ensure that the web application is running smoothly and provides a positive user experience.
There are various tools and technologies available for web stack monitoring, including application performance monitoring (APM) tools, log analysis tools, network monitoring tools, and more. These tools can help automate the monitoring process and provide real-time alerts when issues arise.
Examples of Web stack monitoring tools
Here are some examples of web stack monitoring tools:

•	Nagios: A popular open-source monitoring system that can monitor a wide range of services, including web servers, application servers, and databases.
•	Zabbix: Another open-source monitoring system that supports monitoring of web servers, application servers, and databases. It has a user-friendly interface and can send alerts to multiple channels.
•	Datadog: A cloud-based monitoring platform that offers real-time monitoring of web servers, application servers, and databases. It can provide detailed performance metrics and alerts.
•	New Relic: A cloud-based monitoring platform that offers comprehensive performance monitoring of web applications, servers, and databases. It can monitor transactions, code-level performance, and user experience.
•	SolarWinds: A network and application performance monitoring tool that can monitor web servers, application servers, and databases. It provides comprehensive insights into the performance of the web stack.
•	Splunk: A platform that collects and analyzes data from various sources, including web servers, application servers, and databases. It provides real-time insights and alerts for issues in the web stack.
•	Prometheus: An open-source monitoring system that is specifically designed for monitoring containers and microservices. It can monitor web servers and other components of the web stack.
•	ELK Stack: A collection of open-source tools including Elasticsearch, Logstash, and Kibana that can be used to collect, process, and analyze log data from web servers, application servers, and databases. It can provide insights into system performance and issues.
What is a web server?
A web server is a software application that serves web pages and other web content over the internet. When a user requests a web page from a website, the web server receives the request and responds by delivering the requested content to the user's web browser. The web server software may be installed on a dedicated server machine, or it may be run on a shared server along with other websites. The most commonly used web server software is Apache, followed by Nginx, Microsoft IIS, and others. A web server typically supports multiple programming languages and technologies, such as HTML, CSS, JavaScript, PHP, and databases like MySQL, PostgreSQL, and MongoDB. 
Network basics
What is a protocol
In computing, a protocol is a set of rules and standards that define how devices communicate with each other on a network. A protocol specifies the format and sequence of messages that are exchanged between devices, as well as the actions that should be taken in response to those messages.

Protocols are important because they allow different devices and systems to communicate with each other in a standardized way, even if they are made by different manufacturers or run on different operating systems. Without protocols, it would be difficult to establish and maintain reliable connections between devices on a network.
There are many different protocols used in networking, each with its own specific purpose and set of rules. For example, the Transmission Control Protocol (TCP) is a protocol used for reliable transmission of data over a network, while the Internet Protocol (IP) is a protocol used for routing data packets between devices on different networks.
Some other commonly used protocols in networking include the Hypertext Transfer Protocol (HTTP) for web browsing, the File Transfer Protocol (FTP) for file transfers, and the Simple Mail Transfer Protocol (SMTP) for email.
What is an IP address
An IP address, short for Internet Protocol address, is a unique numerical identifier assigned to each device connected to a computer network that uses the Internet Protocol for communication.
IP addresses are used to identify and communicate with devices on a network. They enable devices to send and receive data packets over the internet, and help to ensure that the data gets delivered to the correct device.
IP addresses are typically represented as a string of four numbers separated by periods (e.g. 192.168.1.1). There are two versions of IP addresses currently in use: IPv4 and IPv6. IPv4 addresses are 32-bit addresses and are expressed in decimal notation, while IPv6 addresses are 128-bit addresses and are expressed in hexadecimal notation.
IP addresses can be either dynamic or static. Dynamic IP addresses are assigned to devices by a DHCP server and can change over time, while static IP addresses are manually assigned to devices and remain the same unless they are manually changed.
IP addresses are an essential part of internet communication, and are used for a variety of purposes including identifying devices on a network, routing data packets between devices, and enabling remote access to devices over the internet.
What is TCP/IP
TCP/IP stands for Transmission Control Protocol/Internet Protocol. It is a set of networking protocols used to facilitate communication between devices on the internet and other computer networks.
TCP/IP is a suite of protocols that includes several different layers, each with its own set of protocols and functions. The four layers of the TCP/IP model are:
Application layer: This layer contains protocols that enable communication between applications running on different devices, such as HTTP for web browsing and SMTP for email.

Transport layer: This layer provides reliable and error-free transmission of data between devices, and includes the Transmission Control Protocol (TCP) and User Datagram Protocol (UDP).
Internet layer: This layer handles the transmission of data packets over the internet and includes the Internet Protocol (IP) as its main protocol.
Network access layer: This layer provides protocols for accessing the physical network, such as Ethernet and Wi-Fi.
TCP/IP is the most widely used networking protocol suite on the internet, and is essential for communication between devices and services on the internet.
What is an Internet Protocol (IP) port?
An Internet Protocol (IP) port is a 16-bit number used to identify a specific process or application running on a device connected to a network.
In networking, communication between devices takes place using Internet Protocol (IP) packets. Each packet contains both the IP address of the device sending the packet and the IP address of the device receiving the packet. In addition, each packet contains a source port and a destination port number.
The source port is a randomly generated number used to identify the process or application that sent the packet, while the destination port is a fixed number used to identify the process or application that should receive the packet.
Port numbers range from 0 to 65,535, with well-known ports (numbers 0 to 1,023) reserved for specific applications and services. For example, port 80 is commonly used for HTTP web traffic, while port 443 is commonly used for HTTPS encrypted web traffic.
IP ports allow multiple applications or services to run on a single device, with each application or service identified by a unique port number. They also enable devices to communicate with each other on a network using a wide variety of protocols and services, each identified by a unique port number.
Load balancer
Load-balancing
Ever wonder how Facebook, Linkedin, Twitter and other web giants are handling such huge amounts of traffic? They don’t have just one server, but tens of thousands of them. In order to achieve this, web traffic needs to be distributed to these servers, and that is the role of a load-balancer.
 
Load balancing is a technique used in computing to distribute workloads across multiple computing resources, such as servers, processors, or network links, in order to improve performance, availability, and reliability.
The basic idea behind load balancing is to distribute incoming requests or traffic across multiple resources so that no single resource is overloaded, and all resources are used efficiently. This can be accomplished in a number of ways, including:
Round-robin: Distributing requests evenly across resources in a rotating fashion.
Least connections: Directing requests to the resource with the fewest active connections.
IP hash: Assigning requests to resources based on the client's IP address.
Load balancing can be used for a variety of purposes, such as improving response times for web applications, reducing downtime by automatically rerouting traffic in the event of a failure, and increasing scalability by adding resources as needed to handle increased demand.
Load balancing can be implemented using hardware or software solutions, and can be integrated into a variety of network architectures, including local area networks (LANs), wide area networks (WANs), and cloud computing environments.
Load-balancing algorithms
There are several load-balancing algorithms used in computing to distribute workloads across multiple computing resources. Some of the commonly used algorithms are:
•	Round-robin: In this algorithm, incoming requests are distributed in a circular order among a set of resources. Each request is sent to the next available resource in the list.
•	Least connections: In this algorithm, incoming requests are distributed to the resource with the least number of active connections. This ensures that heavily loaded resources are not overwhelmed with new requests.

•	IP Hash: In this algorithm, incoming requests are distributed based on the hash value of the client's IP address. This ensures that requests from the same client are always directed to the same resource.
•	Weighted round-robin: This algorithm is similar to round-robin, but assigns weights to each resource based on its capacity or capability. Resources with higher capacity receive more requests.
•	Least response time: In this algorithm, incoming requests are directed to the resource with the fastest response time. This ensures that requests are processed quickly and efficiently.
•	Random: In this algorithm, incoming requests are distributed randomly among a set of resources. This can be useful in situations where resources have similar capacities and workloads.
•	Load-balancing algorithms can be implemented using hardware or software solutions, and can be customized to meet the specific needs of an organization. The choice of algorithm depends on the specific requirements of the workload and the available resources.
What is a database
A database is a structured collection of data that is organized in a way that allows it to be easily accessed, managed, and updated.
In computing, databases are used to store and manage large amounts of information, ranging from customer data for a business to scientific data for research purposes. A database typically consists of one or more tables, each of which contains a set of records with data organized in columns and rows.
Databases are used to store information in a way that is efficient and scalable, making it easy to search, sort, and filter the data. They also allow for data to be easily updated and maintained over time. In addition, databases provide a secure and reliable way to store data, with built-in features for data backup and recovery.
There are several types of databases, including relational databases, NoSQL databases, and object-oriented databases. Each type of database has its own strengths and weaknesses, and is suited to different types of applications and data storage requirements.
What’s the difference between a web server and an app server?
A web server and an app server are two different types of server software that perform different functions in the context of a web application.
A web server is a server software that is designed to serve static content, such as HTML pages, images, and other files, to web browsers over the internet. When a user requests a resource from a web server, the server responds with the requested resource in the form of an HTTP response.
An application server, on the other hand, is designed to execute dynamic applications, which generate content in real-time based on user requests. An app server typically runs on top of a web server and provides additional functionality, such as transaction management, security, and data access. An app server can execute code written in a variety of programming languages, such as Java, Python, or Ruby, and can be used to build complex web applications.
In summary, the main difference between a web server and an app server is the type of content they serve. A web server serves static content, while an app server executes dynamic applications. However, it is common for an app server to be installed on top of a web server, in order to provide additional functionality for building and deploying web applications.
Single point of failure

A single point of failure (SPOF) refers to a component or part of a system that, if it fails, can cause the entire system to fail. In other words, it is a vulnerability in a system that can bring down the entire system if it fails or malfunctions.
Examples of single points of failure can include a single server, network switch, power supply, or even a single employee who is the only one with a specific skill or knowledge required for the system's operation. If any of these components fails, the entire system will fail or become inaccessible.
To minimize the risk of SPOFs, redundancy and backup systems are often implemented. These can include having multiple servers, network switches, power supplies, or having multiple employees with the required knowledge or skills. By eliminating or reducing single points of failure, systems can become more reliable, resilient, and less prone to catastrophic failure.
How to avoid downtime when deploying new code
To avoid downtime when deploying new code, there are several best practices you can follow:
•	Test code changes thoroughly: Before deploying new code to production, it's important to test it thoroughly to identify and fix any bugs or issues that could cause downtime. This can include unit testing, integration testing, and user acceptance testing.
•	Use a staging environment: Use a staging environment that is similar to your production environment to test code changes in a controlled environment before deploying to production. This will allow you to identify and fix issues before they affect your users.
•	Implement a rolling deployment strategy: Instead of deploying new code to all servers at once, use a rolling deployment strategy that deploys the new code gradually, one server at a time. This will minimize the risk of downtime caused by bugs or issues in the new code.
•	Have a rollback plan: In case something goes wrong during deployment, have a rollback plan in place to quickly revert to the previous version of the code. This will help minimize downtime and ensure that your users are not affected.
•	Use monitoring tools: Use monitoring tools to track the performance and health of your system before, during, and after deployment. This will help you identify any issues and quickly address them before they affect your users.
By following these best practices, you can minimize the risk of downtime and ensure a smooth deployment process when deploying new code.
High availability cluster (active-active/active-passive)
A high availability cluster is a group of interconnected computers or servers that work together to provide continuous availability and prevent downtime in case of hardware or software failures. High availability clusters can be configured in two main ways: active-active and active-passive.

Active-active clusters have all nodes actively processing requests and serving clients simultaneously. In this configuration, if one node fails or becomes unavailable, the remaining nodes can continue to handle requests, ensuring high availability and fault tolerance. Active-active clusters can offer better performance and scalability than active-passive clusters because all nodes are processing requests.
Active-passive clusters, on the other hand, have one node that is actively processing requests and serving clients, while the other nodes are in standby mode, ready to take over in case of a failure. In this configuration, if the active node fails or becomes unavailable, the passive node can take over and start processing requests. Active-passive clusters offer a simpler configuration and can be less expensive to implement than active-active clusters.
Both active-active and active-passive clusters provide high availability and fault tolerance, but the choice between the two depends on specific business requirements, performance needs, and budget constraints.
Overall, high availability clusters are an important tool for ensuring continuous availability and minimizing downtime in mission-critical systems.
What is HTTPS
HTTPS stands for Hypertext Transfer Protocol Secure. It is a protocol used for secure communication over the internet. HTTPS is essentially the same as HTTP, which is the protocol used for communication between web servers and clients, but with an added layer of encryption to secure the data being transmitted.
When a client, such as a web browser, makes a request to a web server using HTTPS, the server responds with a digital certificate that includes a public key. The client uses the public key to encrypt a symmetric key, which is then sent to the server. The server decrypts the symmetric key using its private key, and then uses this key to encrypt and decrypt all subsequent data transmitted between the client and server. This process ensures that the data being transmitted is protected from eavesdropping, tampering, and other security threats.
HTTPS is commonly used for secure communication in online transactions, such as online banking, e-commerce, and online payments. It is also increasingly used to secure general browsing on the web, especially for websites that handle sensitive information, such as login credentials or personal information. Using HTTPS is considered best practice for securing web communication and protecting user privacy.


What is a firewall
A firewall is a network security device that monitors and controls incoming and outgoing network traffic based on predetermined security rules. The purpose of a firewall is to create a barrier between an internal network, such as a corporate or home network, and the internet, which is a public network.
Firewalls can be hardware devices or software programs installed on a computer or server. They work by examining the data packets that are transmitted over a network, and applying a set of rules to determine whether to allow or block traffic.
Firewalls can be configured to block traffic based on a range of criteria, such as source IP address, destination IP address, port number, protocol, and specific keywords or patterns in the data. They can also be configured to allow traffic only from trusted sources, such as authorized IP addresses or domains.
Firewalls are an important part of a network security strategy, as they provide a first line of defense against unauthorized access, malware, and other cyber threats. By blocking potentially harmful traffic, firewalls help prevent data breaches, denial-of-service attacks, and other security incidents.
System redundancy
System redundancy refers to the duplication of critical components or processes within a system, in order to minimize the risk of a single point of failure. In other words, redundancy is the provision of backup components, systems or processes that can take over in the event of a failure or malfunction of the primary components.
System redundancy is important for critical systems that require high levels of availability, reliability and fault tolerance.
Mentioned acronyms: LAMP, SPOF, QPS
LAMP: LAMP is an acronym that stands for Linux, Apache, MySQL, and PHP. It is a popular open-source software stack that is commonly used to build web applications.
•	Linux is the operating system
•	Apache is the web server
•	MySQL is the relational database management system (RDBMS)
•	PHP/Python is the programming language used for server-side scripting
SPOF: SPOF stands for Single Point of Failure. It refers to a component in a system that, if it fails, will cause the entire system to fail. Having a single point of failure in a system can be problematic as it can lead to downtime and data loss.

QPS: QPS stands for Queries Per Second. It is a metric used to measure the performance of a system or database in terms of how many queries it can handle per second. This metric is commonly used in web applications and database systems to measure the throughput of a system.

https://imgur.com/
Imgur is an online image hosting and sharing platform. It was created in 2009 by Alan Schaaf as a simple image hosting service, but has since grown into a full-fledged community with millions of users.
Users can upload and share images on Imgur without creating an account, although creating an account allows users to manage their uploads, create albums, and interact with other users. The platform allows users to upload images in a variety of formats, including JPEG, GIF, PNG, and WebM.
Imgur also features a variety of social features, including the ability to comment on images, vote on images using a "like/dislike" system, and share images on other social media platforms. The platform also has a popular "meme" section, which features user-generated content in the form of humorous images with captions.
Imgur is often used by content creators and bloggers as a hosting platform for images, as it allows for easy embedding of images on other websites. Additionally, Imgur's user-generated content often goes viral and is shared across the internet, making it a popular source for entertaining and informative images.

Draw.io for drawing diagrams
https://app.diagrams.net/

AUTHOURS

Benson Mwangi <bensonmwangi102@gmail.com>
Stephanie Iman











