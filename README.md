# AWS-Load-Balancers
AWS Load Balancers: Distribute incoming traffic across multiple targets (EC2 instances, containers, IPs) to ensure high availability, scalability, and fault tolerance in AWS. 

- There are 3 types of LB in AWS :- Application LB , Network LB and GateWay LB

Load Balancer
- 
- Suppose, as a developer we've deployed games app on EC2 instance. Initially there was not much load, just few users were there who were accessing the game. Later the game got popular and load got increased by 100s of users. So our EC2 cannot handle the same as only one EC2 instance cannot serve all users. Due to this, users might face slowness or downtime. 
- To mitigate the same, instead of using one EC2 we can use multiple EC2 and deploy our app on to them and configure load balancer amongst the instances.
- So after deploying LB, users instead of accessing EC2 instance will access LBs from where the request goes to EC2 instances using distribution model manqaging load onto instances
- If all EC2 have same configurations like RAM, CPU, type of OS, then LB mechanism implemented will be "Round Robin" which is basic LB mechanism. Using Round robin users requests gets equally distributed amongst instances. So using this we can provide "High Availability" of our application to users reducing slowness and downtime.
  
- So general technique to have "High Availability" application is using a LB technique. 
  - There are many LBs in market such as Nginx, F5, Envoy, Traffic, etc each of which provides different LB techniques.

- If amongst our 3 instances, 1 is more powerful than others, we can send 50% requests to that EC2 and 25-25% to other 2 :- "Ratio Based LB" or "Weight Based LB"

--------------------------------------------------------------------------------------------------------------------------

7 Layers of OSI Model
-
- How a packet flows from client to server/how packet flows from 7 layers of OSI model? When we open browser and search any site, how our request travel and reach one of our google servers and response is sent back?

- This entire process happens within 7 layers

- User want to access linkedin/shubham315, he will open browser and search the profile, means user will initiate the request. It will travel over internet and it will reach one of the linkedin server and that server will send response back to user with my profile page. 
- Internally request from user travels from 7 different layers and reaches server or application. Here different LBs act on different layers of this OSI model.

- Request started with user accessing my profile

Application Layer
-
  - User while opening the browser will initiate an HTTP request which is "Application layer" (layer7). Here we decide which protocol to use to access server. Protocols are HTTP, SFTP, FTP.
  - So after opening browser, we initiate an HTTP request as our browser is HTTP client.
  - If we dont use browser and use postman, there we can define which protocol we can use.

Presentation Layer
-
  - From application layer, our request goes to presentation layer.
  - The request we're sending needs to be secure or non-secure.
  - For secure one request has to be SSL/TLS based. This is done by presentation layer which takes care of encoding/encrypting our request

Session Layer
-
  - Then request goes to session layer where we create session for our request.
  - Server will here understand things about session that user has initiated. Here we get details like time of request, type, etc.

Transport Layer
-
  - This layer is very critical where request split into multiple packets. This layer ensures request goes from user/client to server securely and in packets of small size.
  - So when we send huge requests to server, there can be delay in response received from server. So if we split request in small packets, server can easily read packets and send response in small packets

Network Layer
-
  - The small packets have to travel from user to server through multiple routers. Request goes to multiple routers.

Data Link Layer
-
  - Here request goes through one of the routers. Our request before reaching physical layer goes to switch then data center and then physical layer

Physical Layer
-
  - Request goes to Physical layer where we have all cables connected to server. Cables to be connected with switch and switch connects to router

- In short, the packet/traffic flow looks like below

Application Layer(7) - Presentation Layer(6) - Session Layer(5) - Transport Layer(4) - Network Layer(3) - Data Link Layer(2) - Physical Layer(1)
-

--------------------------------------------------------------------------------------------------------------------------

Types of LB
-
- There are 3 types of Load Balancers
  - Application LB
  - Network LB
  - GateWay LB
- Now depending on LB and 7 OSI layers we'll decide which LB to use :- ALB, NLB, GWLB

- If we want to perform traffic Load balancing on layer 7, use ALB  (Application layer)
- If we want to perform traffic Load balancing on layer 4, use NLB  (Transport layer)

Application Load Balancer (ALB)
-
- L7 will deal with HTTP traffic in this layer. If we want to perform load balancing at HTTP layer, we use ALB. When user initiates request, if we want to intercept user request at layer 7 and decide upon Load balancing depending upon host, path, domain we can use ALB
- To access amazon.com/payments, my request will go to payment service. If we're accessing LB on amazon.com/transactions, our request will go to "transactions" target group.
  - So with ALB when we access ALB of amazon.com, we can configure it with custom domain of amazon. User will access amazon on different paths depending upon app. So if request is being sent to amazon, then forward it to one particular server only(payments or transactions).
  - So ALB makes decision which type of request to go to which server. As we're doing balancing on app level, its called L7 LB
- At L7, we can intercept HTTP request and read it like what are the request headers, what path user has to access, what is host. We can alo perform ratio based routing.
- ALB makes decision of routing depending upon HTTP requests that we send.
- It also performs SSL offloading, reencrypt.
- Even if we send stale request to LB, LB will initiate secure connection of our server

- ALB is costly as it has advanced capabilities as it intercepts HTTP request and decide which server to forward.
- It is also slow as ALB analyses our L7 and then request gets forwarded to servers. So there is stoppage in between(latency)

Network Load Balancer (NLB)
-
- Suppose, we dont want to perform routing depending on HTTP request that is sent to us.
- Lets say there is NLB and apps under it. When user sends request to NLB, it cannot intercept our HTTP request, means it wont perform any modifications at Layer 7. But when request comes from L7 to L4, NLB plays critical role in transport layer (L4)
- L4 routing is needed in game servers, youtube as transport layer transmits data in small chunks and ensures data is transmitted from user/client to server without any latency or issues or loss of data. This is taken care by NLB ensuring low latency and high data transmission. 
- NLB is used where simple delay is also not expected like gaming, utube, streaming platforms which was there in ALB
- It performs routing based on TCP/UDP patterns
- So to perform load balancing without any interruptions, use NLB
- In real time, request is sent to NLB and depending upon port, IP address will forward requests to our servers

- e.g :- To access youtube, then we can place NLB and depending on request NLB will forward the request.
- NLB is less costly
- It is very fast compared to ALB (No latency)
- It performs routing at TCP/UDP packets
- ** NLB can create sticky sessions. All request from specific user gets tagged to same server

Gateway Load Balancer (GWLB)
-
- Useful when we deal with virtual appliances like VPN, firewall where we can frontface apps with GWLB.
- If for firewall we do ALB, kind of traffic received by firewall ALB cannot handle. Also ALB/NLB doesn't add security
- Using virtual applianceslike VPN or firewall, our traffic has to be highly secure which is offered by GWLB which sends highly encrypted packets to virtual appliances.
- 

When we want to use virtual appliances like VPN or firewall, go for GWLB
We dont want to route traffic or dont want to apply LB techniques at L7, go for NLB
If we want to perform advanced LB, go for ALB
-

--------------------------------------------------------------------------------------------------------------------------

NLB can create sticky sessions. All request from specific user gets tagged to same server. If we're watching long video, all requests goes to one server only from specific user. So we use NLB for content streaming platforms
-
