**What is API versioning?**
API versioning is a method for managing changes to an API over time. 
As APIs grow to meet new business demands, embrace new technologies, or address bug fixes, 
they must be carefully updated to ensure that existing clients can continue to work while new 
features and improvements are enabled.

**When do we think to do API versioning**
-----------------------------------------

when you want to give some additional business or new customer experience to few customers not all but 
also want to keep old business with old customers.Then upgrading the existing version might be 
breaking change so you dont want to touch exsitng business and want to update the business for new customers 
then add versioning will work here so it will be no impact on old customer and new customers can also have new experience.

**How many types of API Versioning**
-----------------------------------
API Versions can be send in below format-
Header
Request param
Path param
Hybrid approach - 2 or more strategy either request param or URI or header

**API Versioning strategy**
---------------------------
1. Managing Multiple Versions
2. Ensuring Backward Compatibility and Avoiding Breaking Changes
3. Balancing the Cost of Versioning and Maintenance

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

One of the most popular service mesh is Istio

    **Between API Gateway and Service Mesh**
    ----------------------------------------
1. API Gateway follows north south Pattern and looks after authentication and authorisation while 
    a service mesh handles functions like load balancing and encryption between services.
2. The service mesh is in its own unique instance as a sidecar proxy, and it is not exposed to external clients 
   but API gateways are exposed to external clients.
3. Service mesh only handles communication between services that make up a system, 
    while an API gateway decouples the underlying system from the API that is exposed to 
    clients (which can be other systems within the organization or external clients).
