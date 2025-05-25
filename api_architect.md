**What is API versioning?**
API versioning is a method for managing changes to an API over time. 
As APIs grow to meet new business demands, embrace new technologies, or address bug fixes, 
they must be carefully updated to ensure that existing clients can continue to work while new 
features and improvements are enabled.

**When do we think to do API versioning**
-----------------------------------------

when you want to give some additional business or new customer experience to few customers not all but 
also want to keep old business with old customers.Then upgrading the existing version might be 
breaking change so you don't want to touch existing business and want to update the business for new 
customers then add versioning will work here so it will be no impact on old customer and 
new customers can also have new experience.

**How many types of API Versioning**
-----------------------------------
API Versions can be send in below format-
Header
Request param
Path param
Hybrid approach - 2 or more strategy either request param or URI or header

**Why API Versioning required**
-------------------------------
Introducing breaking changes (e.g., removing a field, modifying response formats) can 
disrupt client applications.

Versioning enables gradual adoption of new features while maintaining older versions for 
clients that need stability.

Different consumers (mobile apps, web apps, third-party integrations) may have 
dependencies on different API versions.

Deprecate old versions gradually, giving clients time to migrate.

**what is service mesh**
-------------------------
A service mesh is a software layer that handles all communication between services in applications.
This layer is composed of containerized microservices. 
As applications scale and the number of microservices increases, it becomes challenging to monitor 
the performance of the services. To manage connections between services, a service mesh provides 
new features like monitoring, logging, tracing, and traffic control.

**Service Mesh Architecture**
-----------------------------

Following is the Service Mesh Architecture

![img_13.png](img_13.png)

Control Plane - Manages the layer of security and communication rules.
                it works as route53 table in AWS Cloud.
Data plane - sidecars for each service to communicate and transforming the routes.

One of the most popular service mesh is Istio.

**Between API Gateway and Service Mesh**
-----------------------------------------

1. API Gateway follows north south Pattern and looks after authentication and authorisation while 
    a service mesh handles functions like load balancing and encryption between services.
2. The service mesh is in its own unique instance as a sidecar proxy, and it is not exposed to external clients 
   but API gateways are exposed to external clients.
3. Service mesh only handles communication between services that make up a system, 
    while an API gateway decouples the underlying system from the API that is exposed to 
    clients (which can be other systems within the organization or external clients).

**Microservice Design Patterns**
--------------------------------
1. API Gateway - Centralized control for orchestration, log monitoring , error handling
2. Circuit Breaker - To avoid multiple calls in case any service is down.
3. Saga - The saga pattern is used to ensure data consistency across multiple services in a microservices architecture.
   In traditional monolithic systems, transactions are usually managed using a two-phase commit.
   The saga pattern proposes an alternative solution. It suggests breaking a transaction into 
   multiple local transactions.
   Each local transaction updates data within a single service and publishes an event.
   Other services listen to these events and perform their local transactions.
   If a local transaction fails, compensating transactions are executed to undo the changes.
4. Command Query Responsibility Segregation (CQRS)
6. Service Registry - Centralized place where are services registered to discover any service
   by service discovery this can be used.
7. Event-Driven Architecture
8. Domain Driven Architecture
9. Service discovery  - Using Eureka(Used in Barclays)

**Which API Gateways are used in Barclays**
--------------------------------------------
Zuul API Gateway is being used(Spring Cloud Libraries)
Zuul is built to enable dynamic routing, monitoring, resiliency, and security.

**What is eureka server**
--------------------------
Eureka server is used in barclays which contains all information of client and service details
It's a kind of service discovery utility


**CQRS Microservices Design Pattern**
-------------------------------------
    Command Query Responsibility Segregation - 
    
    * Means Write and Read both from separate DB.
      * Write in one DB like MYSQL ---> publish event to event store--->Event store is subscribed by 
        another MONGO db(NO SQL) --->Same data is saved in Mongo DB
      * When Read happens data is fetched from Mongo DB.
    
    **Benefits**
    ------------
    1. it provides clear separation of roles making both operations isolated.
       2. it is beneficial when seperate scaling is needed for reading and writing optimzing both the 
          operations effectively.
       3. All events can be stored in event store for future audit purpose.
    
    **Where can we leverage CQRS**
    ------------------------------
    High-traffic microservices with frequent reads/writes (e.g., e-commerce, banking).
    
    Systems requiring separate scalability for read and write operations.
    
    Event-driven architectures where real-time data updates are needed.

**SAGA**
--------
A saga is a sequence of local transactions. Each local transaction updates the database and publishes 
a message or event to trigger the next local transaction in the saga. If a local transaction 
fails because it violates a business rule then the saga executes a series of compensating 
transactions that undo the changes that were made by the preceding local transactions.

**SAGA vs 2 Phase commit**
--------------------------
SAGA and 2 Phase commit both are used for data consistency and distributed transactions but slightly 
different approach

SAGA  - Each transaction is a kind of local transaction 
2phase commit  works on prepare and commit mechanism

SAGA Architecture

![img_16.png](img_16.png)

2 Phase Commit Architecture

![img_17.png](img_17.png)

Problem with 2 phase commit - 
1. if the coordinator fails then whole flow is disturbed and disrupted.
2. No Automatic Recovery.




**Difference between domain driven and event driven architecture in microservices**
-----------------------------------------------------------------------------------

**When to Use DDD for Microservices-->**
----------------------------------------

**Complex Domains:**
--------------------
If your application deals with intricate business logic and requires a deep understanding of the
domain, DDD can provide a structured approach to model and implement the system.

**Large Systems:**
------------------
When you're building a microservices architecture with multiple services,
DDD can help define clear boundaries and interactions between these services, promoting
modularity and scalability.

**Aligning with Business Logic:**
---------------------------------
DDD encourages aligning software design with business requirements,
ensuring that each microservice encapsulates a specific business capability.

**Decomposing Monoliths:**
--------------------------
If you're migrating a monolithic application to a microservices architecture,
DDD can help identify logical boundaries and ensure each microservice remains cohesive.

**When to use Event Driven Architecture**
-----------------------------------------
Event-driven design for microservices is best suited for scenarios involving real-time processing,
high concurrency, and complex event handling, such as IoT applications, real-time analytics, and systems
requiring asynchronous communication and coordination between teams or different regions.

**What is GRAPHQL**
-------------------
GraphQL is a query language and API specification for building client applications, while
RAML (RESTFUL API Modeling Language) is a specification for defining RESTFUL APIs.
GraphQL focuses on efficient data fetching, while RAML is designed for API design and
documentation.



========================================AWS==========================================================
-----------------------------------------------------------------------------------------------------

Mohammd Naveed sait - Capgemini
https://medium.com/@mohammednaveedsait

**How will you make your application more scalable on high traffic day?**
-------------------------------------------------------------------------

Put your VMs or ECS in autoscaling group and use Load balancer but since cloud is much more
matured now so we can now use
more add ons to manage high traffic.Using load balancer and autoscaling group only will not
keep up scaling my EC2 so below add ons can be used.

During Big traffic event we can-
1. Prewarm load balancer -
2. Scheduled scaling for my autoscaling -
3. Use lightweight AMI for EC2 - The more unnecessary libraries in AMI more time will will take to spin up or scale for EC2. So better to take light weight AMIs.
4. Use RDS proxy to create new connections as high traffic will come.
   RDS proxy will use data base connection pooling if lot of connections are open and then as
   per usage will reuse them instead creating new one. RDS Proxy manages the connection pooling,
   security , high availability.
5. run IEM to handle high traffic - to explore

**Lambda Autoscaling**
----------------------
Concurrency is the number of in-flight requests that your AWS Lambda function is handling at the
same time.
For each concurrent request, Lambda provisions a separate instance of your execution environment.
As your functions receive more requests,
Lambda automatically handles scaling the number of execution environments until you reach your account's
concurrency limit.

By default, Lambda provides your account with a total concurrency limit of 1,000 concurrent executions across all functions in an AWS Region.
To support your specific account needs, you can request a quota increase and configure
function-level concurrency controls so that your critical functions don't experience throttling.

    **Understanding and visualizing concurrency**

Lambda invokes your function in a secure and isolated execution environment. To handle a request, Lambda must first initialize an execution environment
(the Init phase), before using it to invoke your function (the Invoke phase):

![img.png](img.png)
**Execution Environment Creation**
![img_1.png](img_1.png)

As mentioned in the diagram only 6 instances of execution environment is created for 10 request.
Execution environment is created if no instances are available else reuse the available execution environment.

**AWS Lambda Execution Time Limit**
-----------------------------------
AWS Lambda has a configurable maximum execution time limit of up to 15 minutes. If this limit is reached,
the function will be stopped forcefully by AWS. This means that long-running processes are not easily
possible with Lambda.

    **Understanding reserved concurrency and provisioned concurrency**
--------------------------------------------------------------------------

By default, your account has a concurrency limit of 1,000 concurrent executions across all functions
in a Region.
Your functions share this pool of 1,000 concurrency on an on-demand basis.
Your functions experiences throttling (that is, they start to drop requests) if you run out of
available concurrency.

There are two types of concurrency controls available:
reserved concurrency and provisioned concurrency.

**reserved concurrency**
------------------------

* Use **reserved concurrency** to reserve a portion of your account's concurrency for a function.
* This is useful if you don't want other functions taking up all the available unreserved concurrency.
* When you dedicate reserved concurrency to a function, no other function can use that concurrency.

**Provisioned concurrency**
----------------------------

Use **provisioned concurrency** to pre-initialize a number of environment instances for a function.
This is useful for reducing cold start latencies.

if you have 1000 concurrency limit and you have provisioned 400 units of provisioned concurrency to
one lambda it means that
lambda can use 400 units of provisioned concurrency but if in case more request then it has to use
unprovisioned concurrency but with cold start problem.


* You use reserved concurrency to define the maximum number of execution environments
  reserved for a Lambda function.

* However, none of these environments come pre-initialized. As a result, your function invocations may
  take longer because Lambda must first initialize the new environment before being able to use it
  to invoke your function. When Lambda has to initialize a new environment in order to carry out an
  invocation, this is known as a cold start. To mitigate cold starts, you can use provisioned concurrency.

* Provisioned concurrency is the number of pre-initialized execution environments that you want to
  allocate to your function. If you set provisioned concurrency on a function, Lambda initializes
  that number of execution environments so that they are prepared to respond immediately to function
  requests.

* Using provisioned concurrency incurs additional charges to your account.

MAE -In MAE project no reserved concurrency is configured only Unreserved concurrency is mentioned
with 950 Limit.

**Difference between SQS and SNS**
----------------------------------

SQS and SNS are part of the core of Amazon's serverless offering.

**SQS**
-------

Saves messages in a queue and waits for them to be picked up. SQS is a pull-based service that scales
elastically.
SQS uses queues to publish messages
![img_10.png](img_10.png)
The message remains in the queue for a defined time (by default 4 days, maximum 14 days)
SQS offers many capabilities for retrying messages with its redrive policy. You can define several
retries and a dead letter queue in case messages are failing.
Dead letter queues (DLQ) are used to handle messages with errors.
Relation Ships - Many to One
When Notification reached to Microservices , messages are polled from SQS.


**SNS**
-------

Forward messages to subscribed consumers. SNS is a pub/sub service that uses topics to separate
messages into channels.
SNS uses topics to publish messages
Relation Ships - Many to Many


FanOut Design Pattern
----------------------
SQS are not suppose to send to multiple microservice.its P2P so only 1 microservice it will send.

SNS are suppose to subcribed multiple Queues and each Q is owned by microservice.Each MS will have its
own Qs

![img_9.png](img_9.png)

SNS uses A2A or A2P sending methods
A2A -Application to Application.Destination are AWS Lambda,SQS
A2P - Application to person.Destination are SMS and Emails.

**FAN Out Design Pattern**
--------------------------

FAN Out Design Pattern uses asynchronous communications between microservices
Loosely coupled communications between different systems.

Guide to understand FAN OUT Design Pattern

https://medium.com/aws-lambda-serverless-developer-guide-with-hands/publish-subscribe-fan-out-pattern-in-serverless-architectures-using-sns-sqs-and-lambda-bccaa3abac9e

**Advantage of Fanout design Pattern**
---------------------------------------
Decoupled microservices
each microservice can be scaled independently
Publisher need not to know who is consuming his message.
Subscriber need not to know who is publishing the message.
The whole communication is asynchronous
Each service can be scaled independantly and decoupled with each other.



**DLQs**
--------

When there is any failure in publishing any message to SNS then messages is delivered to DLQ topic
Once DLQ recieved failed messages ,RTB team manually re-triggered messages.


**AWS Cloud Migration Techniques**
----------------------------------
Migration from on premises to AWS Cloud
You can migrate any workload – applications, websites, databases, storage, physical or virtual
servers – and even entire data centers from an on-premises environment.
<TBC>

**Java 17 features**
--------------------
1. Pattern Matching for Switch (Preview) - we can use type also as given below
------------------------------------------------------------------------------

    public String checkObject(Object obj) {
            return switch (obj) {
            case Human h -> "Name: %s, age: %s and profession: %s".formatted(h.name(), h.age(), h.profession());
            case Circle c -> "This is a circle";
            case Shape s -> "It is just a shape";
            case null -> "It is null";
            default -> "It is an object";
        };
    }

2. Sealed Classes
-----------------

    The syntax for declaring a sealed class involves using the sealed modifier before the class 
    keyword. Additionally, you need to specify which subclasses are allowed to extend the 
    sealed class using the permits keyword followed by the list of permitted subclasses.
    
    Here’s an example:
    
    public sealed class Shape permits Circle, Square, Triangle {
    // Class members and methods
    }
    
    
    * Sealed classed can helps to maintainability and encapsulation of code
      * It also ensures that unnecessary classes cannot inherit the super class.


**Difference between BDD and TDD**
----------------------------------
BDD uses tools like Cucumber or SpecFlow to write tests in a "Given-When-Then" format,
making the specifications executable and verifiable.
Feature Files:
--------------
These files, often written in Gherkin syntax, define user stories and scenarios, outlining
the desired behavior of the software.
Step Definitions:
-----------------
These map the Gherkin steps to actual test code, linking the human-readable language with
executable tests.
Reporting Tools:
----------------
These tools visualize test results and track progress, offering insights into the health and
stability of the application.

**TDD (Test-Driven Development)**
---------------------------------
Focuses on writing tests before code, ensuring functionality and
aiding in design, while BDD (Behavior-Driven Development) emphasizes system behavior from a user
perspective, promoting collaboration and using natural language.

**Idempotent**
--------------
GET , PUT, HEAD,DELETE
These methods are considered as idempotent as no effect on repeated invocation call.

POST and PATCH are considered as not Idempotent as repeated invocation can
lead to multiple record creation.

**How to Monitor AWS Lambda Response time**
-------------------------------------------

AWS X Ray - This is used to monitor real time metrics of performance and response time for
serverless applications in distributed Environment.

Use AWS X-Ray for end-to-end tracing, CloudWatch Logs for detailed insights into execution,
and CloudWatch metrics for overall performance analysis, including invocation duration and
error rates.

AWS Lambda automatically sends metrics to CloudWatch, including invocation duration, error rates,
and concurrency.

**How can you improve AWS Lambda performance Issues**
------------------------------------------------------

Focus on optimizing memory allocation, minimizing cold starts, reducing package size, and
utilizing features like provisioned concurrency and connection reuse.

For Example in MAE project we have done these things

**Lambda Layers:**
Use Lambda Layers to share code and dependencies between multiple functions, reducing deployment
artifact size and improving cold start times. when you will open your lambda in AWS you will layers info
in layers.

**Provisioned Concurrency:**
Allocate pre-initialized execution environments to your function, ready to respond to incoming
requests immediately. Be aware that this incurs additional charges.

**Reduce Package Size**
Keep your package as light as possible to move and work lambda faster.
Move any shared code or functionality to common lambda layer like JKS file or pem file to common
lambda layer

**Optimize memory allocation**
Allocate more memory to your lambda but not too much only that is required but incase of performance
issue increase little bit of memory and check the performance you will get it.

Memory is like fuel for your lambda

in MAE project for one of the AIP Lambda we have allocated this much memory
Memory - 2048 MB
Ephemeral Memory - 512MB

**Minimize Cold Starts**
Allocate some provisioned concurrency to get rid of cold start problem.

**Leverage AWS X-Ray for tracing**
Using AWS X-Ray for tracing helps you make your AWS Lambda functions work faster.
Setting up an X-Ray shows you how your functions run and where they might be slowing down.
You can see the whole path of each request and find out what’s causing delays.

**what is timeout in AWS Lambda**
---------------------------------
20 seconds we have kept in config.

**Difference between Authorization and Authentication**
-------------------------------------------------------
Authentication verifies a user's identity (who they are), while authorization determines what
actions or resources they are allowed to access after being authenticated (what they can do).

**what is the execution time limit for any Lambda**
---------------------------------------------------
15 minutes , after 15 minutes lambda got terminated and may encounter 409 request

The HTTP 409 status code, known as "Conflict," indicates that the client's request
couldn't be completed due to a conflict with the current state of the resource on the server

**Reserved Concurrency and Provisioned Concurrency**
----------------------------------------------------
Use **reserved concurrency** to reserve a portion of your account's concurrency for a function.
This is useful if you don't want other functions taking up all the available unreserved concurrency.

Use **provisioned concurrency** to pre-initialize a number of environment instances for a function.
This is useful for reducing cold start latencies.

if you have allocated 400 reserved concurrency to lambda 1 and 400 to lambda 2 and
kept 200 concurrency as unreserved then in case-
1. if lambda 1 or 2 get more request and 400 concurrency limits are already reached then this function
   will experience throttling and started failing request.


**How much is the max execution time for AWS Lambda**
----------------------------------------------------
15 minutes is the max time for lambda execution, after his lambda will autoterminate
if you want to extend more time either use step function to chain your lambdas or use EC2,
Fargate or ECS for heavy longer running time.


**How to use step function to chain lambda for longer running**
---------------------------------------------------------------
you can break your tasks in to multiple small tasks and each task will be
executed by one lambda.
you can create one step function to give instructions to run lambdas to run one by one or paralley.

Each lambda will run for 15 minutes and then you can run and finish your tasks effectively.

**Can I run my aws lambdas synchronous way**
--------------------------------------------

Yes like below

{
"StartAt": "StepOne",
"States": {

            "StepOne": {
            "Type": "Task",
            "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:Lambda1",
            "Next": "StepTwo"
            },

            "StepTwo": {
            "Type": "Task",
            "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:Lambda2",
            "Next": "StepThree"
            },

            "StepThree": {
            "Type": "Task",
            "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:Lambda3",
            "End": true
        }
    }
}

**How to run in parallel same lambdas**
---------------------------------------

{
"StartAt": "RunInParallel",
"States": {
"RunInParallel": {
"Type": "Parallel",
"Branches": [
{
"StartAt": "Lambda1",
"States": {
"Lambda1": {
"Type": "Task",
"Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:Lambda1",
"End": true
}
}
},
{
"StartAt": "Lambda2",
"States": {
"Lambda2": {
"Type": "Task",
"Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:Lambda2",
"End": true
}
}
},
{
"StartAt": "Lambda3",
"States": {
"Lambda3": {
"Type": "Task",
"Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:Lambda3",
"End": true
}
}
}
],
"Next": "FinalStep"
},
"FinalStep": {
"Type": "Pass",
"Result": "All Lambdas Finished",
"End": true
}
}
}

**Concurrency in Dynamo DB**
----------------------------
Concurrency can be handled in DynamoDB using Optimistic Concurrency.
when you save any item in dynamodb the version is saved for the first time.
when you update it the same version is fetched from Dynamo DB and after update when its going to save
it will check if the same version  is there then the same record is updated else concurrency exception
is thrown.

Everytime any record is updated version number is updated everytime.


Sample dynamoDB model

@DynamoDBTable(tableName="ProductCatalog")
public class CatalogItem {

    private Integer id;
    private String title;
    private String ISBN;
    private Set<String> bookAuthors;
    private String someProp;
    private Long version;

    @DynamoDBHashKey(attributeName="Id")
    public Integer getId() { return id; }
    public void setId(Integer Id) { this.id = Id; }

    @DynamoDBAttribute(attributeName="Title")
    public String getTitle() { return title; }
    public void setTitle(String title) { this.title = title; }

    @DynamoDBAttribute(attributeName="ISBN")
    public String getISBN() { return ISBN; }
    public void setISBN(String ISBN) { this.ISBN = ISBN;}

    @DynamoDBAttribute(attributeName = "Authors")
    public Set<String> getBookAuthors() { return bookAuthors; }
    public void setBookAuthors(Set<String> bookAuthors) { this.bookAuthors = bookAuthors; }

    @DynamoDBIgnore
    public String getSomeProp() { return someProp;}
    public void setSomeProp(String someProp) {this.someProp = someProp;}

    @DynamoDBVersionAttribute
    public Long getVersion() { return version; }
    public void setVersion(Long version) { this.version = version;}
}

**Sample AWS Lambda code**
----------------------------

Please consider below step function code to call lambda and return the value

        {
        "Comment": "A simple Step Function that invokes a Lambda function",
            "StartAt": "InvokeLambda",
                "States": {
                    "InvokeLambda": {
                        "Type": "Task",
                        "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:YourLambdaFunctionName",
                        "InputPath": "$",
                        "ResultPath": "$.lambdaResult",
                        "End": true
                    }
            }
        }



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


