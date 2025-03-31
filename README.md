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

