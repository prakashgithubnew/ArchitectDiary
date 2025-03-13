**This repo is for Architect Level Discussions and Learnings.**
===============================================================

**What are cloud-native applications?**
---------------------------------------
* Cloud-native applications are software programs that consist of multiple small, 
  interdependent services called microservices. 
* Traditionally, developers built monolithic applications with a single block structure 
  containing all the required functionalities. 
* By using the cloud-native approach, software developers break the functionalities into 
  smaller microservices. 
* This makes cloud-native applications more agile as these microservices work independently 
  and take minimal computing resources to run.

**Cloud-native applications compared to traditional enterprise applications**
------------------------------------------------------------------------------
* Traditional enterprise applications were built using less flexible software development 
  methods. 
* Developers typically worked on a large batch of software functionalities before releasing 
  them for testing. 
* As such, traditional enterprise applications took longer to deploy and were not scalable.
* On the other hand, cloud-native applications use a collaborative approach and are highly 
  scalable on different platforms. 
* Developers use software tools to heavily automate building, testing, and deploying procedures
  in cloud-native applications. 
* You can set up, deploy, or duplicate microservices in an instant, an action that's not 
  possible with traditional applications. 

**what is regression testing**
-------------------------------

Testing of new code or bug fixes to check if those fixes are impacting any other functionality 
of application

**Tools and Utilities which are provided by Cloud Natives are**
---------------------------------------------------------------
    CI/CD
    Jenkins
    Containers
    Microservices
    Data Bases
    Automated Build
    Automated Deployment
    Orchestration Service like kubernetes

**What is cloud-enabled?**

    Cloud-enabled applications are legacy enterprise applications that were running on an 
    on-premises data center but have been modified to run on the cloud. 
    
    This involves changing part of the software module to migrate the application to 
    cloud servers. You can thus use the application from a browser while retaining 
    its original features.
    Using cloud enabled we cannot leverage the features of scalability, flexibility and resilience , latency handling.


**Cloud native compared to cloud enabled**

    The term cloud native refers to an application that was designed to reside in the cloud 
    from the start. Cloud native involves cloud technologies like 
    microservices, container orchestrators, and auto scaling. 
    A cloud-enabled application doesn't have the flexibility, resiliency, or scalability of its 
    cloud-native counterpart.

    This is because cloud-enabled applications retain their monolithic structure even 
    though they have moved to the cloud.

**What are the bottlenecks of microservice architecture**

    Unlike monolithic applications, microservices communicate over a network (usually via 
    REST APIs, gRPC, or messaging queues). If these calls are slow, the whole application 
    feels sluggish.

    Few More Bottlenecks are below

1. **Communication Overhead**
   Microservices interact over the network, which introduces latency and increased response times compared to monolithic architectures.
   Network failures and serialization/deserialization costs can slow down performance.
2. **Data Management Complexity**
   Each microservice may have its own database, leading to data inconsistency and distributed data management challenges.
   Cross-service transactions (e.g., distributed transactions using Saga pattern) can be complex and slow.
3. **Dependency Management**
   Versioning and compatibility issues arise when different services evolve at different speeds.
   Backward compatibility needs to be maintained, making updates slower.
4. **Service Discovery & Load Balancing**
   Identifying the right service instance (especially in a dynamic cloud environment) can be a challenge.
   Load balancing between instances must be handled efficiently to prevent uneven workload distribution.
5. **Monitoring & Debugging**
   Since requests span multiple services, tracking an issue requires distributed tracing.
   Centralized logging and monitoring are necessary but add complexity.
6. **Deployment & Configuration Management**
   Deploying multiple microservices independently requires robust CI/CD pipelines.
   Configuration management across multiple services can become difficult.
7. **Security Risks**
   Microservices expose multiple endpoints, increasing the attack surface.
   Ensuring secure authentication and authorization across services (e.g., using OAuth, JWT) adds overhead.
8. **Resource Utilization**
   Running multiple services means higher CPU, memory, and networking overhead.
   Inefficient scaling strategies can lead to resource wastage.

**Why It Happens:**

    •	Too many synchronous (blocking) API calls
    •	Network latency
    •	High dependency between services

**How to Fix It:**

    ✅ Use asynchronous communication (e.g., Kafka, RabbitMQ) to avoid waiting for responses
    ✅ Reduce unnecessary inter-service calls (combine multiple calls into one if possible)
    ✅ Implement caching to avoid calling another service for the same data repeatedly
    ✅ Design should adhere proper principles of DDD as poor DDD will lead to performance 
        issues in microservices.
    ✅ To prevent bottlenecks in a microservice architecture, it's crucial to define clear 
        boundaries between services. Each microservice should have a single responsibility and 
        manage its own data domain. 
        This approach, known as the Single Responsibility Principle, reduces the likelihood of 
        tightly coupled services that can create a domino effect of delays when one service experiences issues. 
        By maintaining loose coupling and high cohesion within services, 
        you enhance the system's resilience and agility
     ✅ Use Saga Pattern or Orchestration Strategy to handle distributed transactions.
     ✅ Use Database per Service pattern
     ✅ Maintain API contracts using OpenAPI (Swagger) to track changes.
     ✅ Use service meshes (Istio, Linkerd) for better service-to-service communication.
     ✅ Use Service Discovery Tools like Consul, Eureka, or Kubernetes Service Discovery to dynamically locate services.
     ✅ Use CI/CD pipelines (Jenkins, GitHub Actions, GitLab CI) to automate deployment.
     ✅ Use OAuth 2.0 & JWT for secure authentication and authorization.
     ✅ Implement API Gateway with rate limiting and WAF (Web Application Firewall).
     ✅ Use Auto-scaling (Kubernetes HPA, AWS Auto Scaling) to allocate resources dynamically.
     ✅ Implement Serverless Architectures where applicable (AWS Lambda, Azure Functions).

**Below Principles Should be followed while designing DDD or Microservice**

    Define Boundaries  -Single responsibility principle

    Decouple Services - Achieve this by using asynchronous communication between services.

    Implement APIs - Utilizing Application Programming Interfaces (APIs) effectively is a key strategy in managing 
                 microservice dependencies. Use backward compatibility so if any updates going this 
                 will not impact any flow 

    Monitor Traffic - Monitoring traffic flow between microservices is critical for identifying and addressing bottlenecks. Implementing a monitoring solution that provides real-time insights into service interactions can 
                        help you detect issues early and respond promptly.

    Scale Dynamically - Dynamic scaling is a powerful tool in preventing bottlenecks in a microservice 
                        architecture. By using container orchestration platforms like Kubernetes, 
                        you can automatically scale services up or down based on demand.

    Use Circuit Breakers - Implementing circuit breakers is an effective way to manage microservice dependencies and prevent bottlenecks. 
                            A circuit breaker is a design pattern that monitors for failures and temporarily disables service operations if a 
                            threshold of errors is reached, allowing the system to continue functioning while the issue is resolved. 
                            This prevents failures from cascading across services and creating system-wide bottlenecks.

**AWS Disaster Recovery Architecture and Strategies**
------------------------------------------------------

https://www.youtube.com/watch?v=_4hESnziWIE

![img_3.png](img_3.png)

1. Different Strategies for AWS Disaster Recovery

**Backup and Restore(active/passive)**
--------------------------------------
* active/passive means production servers will be active and DSR servers will be passive
* active/active means production and DSR servers will be active both.
* cheapest option
* will take hours to restore
* it will take backup and restore


**Pilot light(active/passive)**
--------------------------------
1. Much Faster compared to back up and restore
2. More Costlier than back up and restore
3. Can restore live data


**warm standby(active/passive)**
--------------------------------
1. preety fast than previous two options
2. Always running but for smaller business and for critical business.
3. More costlier than other 2s.


**Multi site(active/active)**
-----------------------------
* zero downtime
* zero data loss
* mission critical service
* high costly
* always running


![img_6.png](img_6.png)


we will study how this DSR works but before that we need to understand few terms before moving ahead.

**what is EBS Volume**
----------------------

* An Amazon EBS (Elastic Block Storage) volume is a durable, block-level storage device that you can attach to your Amazon 
  EC2 instances, acting like a virtual hard drive for persistent storage
* EBS volumes store data persistently, meaning the data remains even if the EC2 instance is 
  stopped or terminated.
* You can attach EBS volumes to EC2 instances, allowing you to extend the storage capacity of 
  your virtual machines.
* EBS volumes are replicated within an Availability Zone to ensure high availability and durability.

**what is EBS Snapshot**
-------------------------
* An Amazon EBS (Elastic Block Storage) snapshot in AWS is a point-in-time copy of an EBS volume, 
  acting as a backup that can be used for data protection, disaster recovery, and migrating data.
* An EBS snapshot is a backup of your EBS volume, which is a virtual hard drive for your Amazon EC2 
  instances.

**what is EFS File System**
---------------------------
Amazon Elastic File System (EFS) is a serverless, fully elastic file storage service that allows you to 
share files across multiple AWS compute instances and on-premises servers, without needing to 
provision or manage storage capacity

**what is DB Snapshot**
-----------------------
In AWS, a DB snapshot is a point-in-time backup of a relational database instance, 
capturing all data and configuration settings, allowing for quick recovery or restoration to a 
specific state.

**Backup and restore Strategies** 
---------------------------------

![img_7.png](img_7.png)


**How to run spring boot application in aws**
---------------------------------------------
1. One way
------------
create spring boot application and prepare jar
create one EC2 instance and get the public IPV4 DNS address
using this address as above get login to EC2 instance using ppk auth
copy jar to ec2 instance using winscp
run the jar in ec2 instance and using the IPV4 address hit the address and check the URL

2.Second way
-------------
create spring boot jar and add in to your docker.
Create one task definitions and add docker image to this task.
Create one task and add above tasks def in to it.
Create one service and add same task as above.
create one ECS cluster and add above service to this ECS.

Once ECS is created wait for service to get up and use public URL and hit in browser , it shud be runnblae.

**AWS Region , AZ and VPC**
----------------------------


**Difference between EC2 on ECS and Fargate on ECS**
--------------------------------------------------

EC2 is mainly VM Machines or compute services where as ECS is used to orchestrate EC2 instances.You can run ECS containers on EC2 instances, or on AWS Fargate, 
a serverless compute engine. AWS Fargate is a serverless compute engine that you can use with ECS to run containers without managing servers or clusters of EC2 instances.

ECS stands for “Elastic Container Service.” Where EC2 uses virtualization and virtual machines (VMs), Amazon ECS is used to manage Docker container applications. 
It is a fully managed container orchestration service that functions in similar fashion to Kubernetes. Amazon ECS orchestrates Docker containers running via Amazon EC2.
Rather than deploying a new EC2 instance to scale up, Amazon ECS uses container clusters. Each cluster contains multiple EC2 instances, governed by the Amazon ECS orchestrator 
to facilitate scaling and failovers. ECS works like a control plane only.
In summary, ECS allows companies to deploy containerized applications and orchestrate them easily, without the infrastructure management burden.

when we create any tasks def on ECS cluster it asks for launch types which are of 2 types
1. Fargate  - ECS will manage all the EC2 instances and you dont need to manage at your won.Fargate will provision EC2 instances as per demand and requriement.                                 
2. EC2 instances - you will need to manage everything at your own like security groups , etc.

when you opt EC2 it's a kind of independent instances which are running your docker images but its not managed ones , you need to manage the capacity , memory, security 
patching AMIs and all will be taken care by you as you are the driver.

when you opt Fargate then its same as serverless lambda functions where you will tell ECS how many docker images you need to run and all will be 
taken care by AWS to find and run EC2 instances for you as per your requirement.

**EKS vs ECS**
--------------
https://www.youtube.com/watch?v=o73kDW0xqlg&t=45s


ECS and EKS are the container services which are used to manage the containers.
Lest suppose you have 4-5 microservices whcih you wanted to dpeloy on AWS using each service in one container. you have chosen EC2 server to deploy these containers in to it.
But what happen when EC2 server limitation reaches if we need to deploy our next container?
who manages these EC2 available resources?
what happen when container crashes?
in peak hours how would you scale up and scale down instances during peak and low traffic?
Load balancing the traffic?


Difference between ECS and EKS

ECS is like control plane and works like a side car.
EKS - <will discuss >


**What is API Gateway and why it is useful for AWS Cloud Infrastructure**
-------------------------------------------------------------------------
API Gateway reduces too many Interservice call
API Gateway manages the  rate limiting and WAF (Web Application Firewall).
API Gateway: Aggregate requests and reduce multiple calls using tools like Kong, Apigee, 
            or AWS API Gateway.
API gateway - manages all security at one place.
API gateway helps in routing the traffic

**How Oauth works in API security**
-----------------------------------
Refer the diagram below to understand the flow

![img_8.png](img_8.png)

There are mainly below parties involved in authorization process

Application
Authorisation server
Resources - which are protected
End user










