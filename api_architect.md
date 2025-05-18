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


**is there any limit on request and response size?**
----------------------------------------------------
Browser Limit: Most modern browsers limit URL length to about 2000–8000 characters.

Internet Explorer: ~2083 characters.

Chrome, Firefox, Edge: ~8000 characters, but still best to stay under 2000.

Server Limit: Web servers (e.g., Apache, Nginx) and API gateways may also impose limits.

API Gateway/Proxy Limits
Some API management layers (like AWS API Gateway, Azure API Management) may limit URL or header size.

Example: AWS API Gateway has a limit of 10 KB for request headers.

**what is the difference betweeen TLS and mTLS**
-------------------------------------------------
TLS where only server certificate will be validated and verified
mTLS where client and server both certificates are validated and verified.

**How mTLS works?**
-------------------
in mTLS clients send his certificate to server for validation and server sends his certificate for validation to client.

How client generates the certificates?
1. Client generate the private key through Open SSL.
   openssl genrsa -out client.key 2048
    private key is stored in client.key file
2. Request CSR(Certificate signing request) using private key generated in first step
   openssl req -new -key client.key -out client.csr
    you will be prompted to enter deails as below
   Country Name (C)       : IN
   Organization Name (O)  : Example Corp
   Common Name (CN)       : client-api-user
3. Submit CSR to the CA
4. CA will issue a Client Receives Signed Certificate
   You’ll receive:

client.crt (the signed client certificate)

Optionally a CA chain (e.g., ca.pem or intermediate.crt)
5. Now you can make a request like below
   curl https://secure-api.example.com \
   --cert client.crt \
   --key client.key \
   --cacert ca.crt
6. The server on the other side will validate this certificate and grant access.

**How SSL/TLS handshake is done**
---------------------------------
SSL/TLS Hand shake means only server certificate will be verified at client end
1. During the SSL handshake, the server sends its digital certificate (and optionally intermediate certificates).
2. The client reads the Issuer field from the server certificate. This tells the client who signed this certificate (i.e., the CA).
3. The client checks its trusted certificate store (local store of root CA certificates) to find:
    A root CA certificate that directly signed the server certificate.
4. The client uses the public key of the issuing CA (found in the CA certificate) to verify the digital signature on the server certificate.
    If the signature is valid, it proves that the server certificate was indeed signed by the CA and hasn’t 
     been tampered with.

**How server generates the certificates at their end?**
--------------------------------------------------------
1. Server uses OPENSSL to generate the public and private key.
   
   Private key: Kept secret on the server
   Public key: Shared with the Certificate Authority (CA) to create a certificate

2. The server sends a Certificate Signing Request (CSR) to a CA, which includes:
Public key
Organization/domain info (e.g., api.example.com)
Other metadata (e.g., location, algorithm used)
3. CA verifies the request and generate the certificate
4. The server sends its certificate to client , which includes its public key. 

**How JWT Token works in Rest API**
------------------------------------
1. Client is onboarded and gets the client id and secret key
2. Once these above are issued client then login using this and call goes to aurthorization server
3. Authorisation server verifies the detaisl and sends the oauth url
4. Then client send request to oauth URL and gets the token(Auth server signs the JWT with its private key.)
5. This token is send back to client for API access
6. Further client uses this token and put in header for access to APIs.
7. Any resource server can verify the jwt token using the public key.
8. if verified then only authrorisation part is taken care.
   

JWT Token never contains the public or private key


