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
