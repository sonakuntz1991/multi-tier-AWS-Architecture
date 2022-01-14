                                               #Multi-tier AWS Architecture
                                                           
Data Service Group has a client that is running an e-commerce. This client wants to run their application with the whole infrastructure on AWS. Basically, we need to build a multi-tier architecture that is used in a client-server application such as a web application that has the frontend, the backend and the database. This architecture is a shift from the monolithic way of building an application where the frontend, the backend and the database  are all sitting in one place. With that, we need to take these into consideration. 

Security: We want to design an infrastructure that is highly secured and protected from the prying eyes of bad actors. As much as possible, we want to avoid exposing our interactions within the application over the internet. This simply means that the application will communicate within themselves with a private IP. The backend and the database tier will also be in the private subnet because we do not want to expose them over the internet. We will set up the Bastion host for remote SSH and a NAT gateway for our private subnets to access the internet. 

Scalability & Fault Tolerant: Each tier of this architecture can be scale horizontally or vertically to support the hike in traffic and request demand coming to it. This can easily be done by adding an Auto Scaling Group and a load balancing with a health check. For instance, assuming we have two EC2 instances serving our backend application and each of the EC2 instances is working at 80% CPU utilization, we can easily scale the backend tier by adding more EC2 instances to it so that the load can be distributed. We can also automatically reduce the number of the EC2 instances when the load is less. This makes  our infrastructure to comfortably adapt to any unexpected change both in traffic and fault.

High Availability: with the traditional data center, our application is sitting in one geographical location. If there is a nature deserter like earthquake, flooding or even power outage in that location where our application is hosted, our application will not be available. With AWS, we can design our infrastructure to be highly available by hosting our application in different locations known as the availability zones.

Modularity: This shift is going to make our infrastructure designed to be highly available and fault tolerant. With that, we’re going to modularize our application such that each part can be managed independently of each other. Modularity enable teams to focus on different tiers of the application and changes are made as quickly as possible. Also, modularization helps us recover quickly from an unexpected disaster by focusing solely on the faulty part.

Basically, we need these services and more;
- a vpc,
- couple subnets
- an elb (elastic load balancer) to stay in front of the webserver instances.
- an autoscalling group to scale up and scale (horizontal) down our instances accordingly. (cpu over usage, instance terminate)
- couple databases (RDS with PostgreSQL)
- cloudwatch for this app monitoring.
- We need a type of notification when our system is running (new instances getting created, instances getting terminated). And for that we will need a notification system like: sns (simple notification service)
- The domain will be jkdhhjfhjfhf.com and to get or purchase this domain, we will need the route 53 service.
-We can also create a dns record with this service.
- Our instances will generate log messages that will need storage and for storage we can use the ebs and s3 bucket
- Also our instances will be serving the same content so we need a share filesystem between those instances and for that we will use efs service.
- We need to manage who can access these infrastructure thru the console and to do that we need to configure access using IAM service.
- Our instance will need access to s3 bucket for backup and logs and to do that, we need to create IAM roles.

To make sure we can recreate all these without manual effort, we will use terraform to write the whole infrastructure as code and automate the process.




![My Blank diagram - Page 1 (1)](https://user-images.githubusercontent.com/94230928/149515221-5129ed8a-81bb-4c38-a0d7-a933bfcce8ab.png)



