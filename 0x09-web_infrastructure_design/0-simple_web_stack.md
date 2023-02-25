What is a server
Servers are physical machines (as hardwares), virtual machines or softwares (computer programs) that serve or provide functionality to other programs or devices called “clients”. The term server comes from queuing theory used in Kendall’s notation, where servers serve or process the clients requirements in the same way as a telephone operator, a cooker or a production machine process incoming orders, having in mind its capacity and service process time.

A computer can function as a server, and a server can be a computer, both of them being built up with hardware and software. However, the main difference between these two is the capacity and computer power servers have. In other words, servers are computers on steroids with faster processing capacity. They are usually stored in data centers racks (stacks of servers piled one on top of each other).

On the other hand, virtual servers function more like virtual machines, or virtual computers. These are a virtual representation of the physical servers, having their own operating system and applications (Posey, 2021).


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
