**How will you make your application more scalable on high traffic day?**
-------------------------------------------------------------------------

Put your VMs or ECS in autoscaling group and use Load balancer but since cloud is much more matured now so we can now use 
more add ons to manage high traffic.Using load balancer and autoscaling group only will not keep up scaling my EC2 so below add ons can be used.

During Big traffic event we can-
1. Prewarm load balancer - 
2. Scheduled scaling for my autoscaling -
3. Use lightweight AMI for EC2 - The more unnecessary libraries in AMI more time will will take to spin up or scale for EC2. So better to take light weight AMIs.
4. Use RDS proxy to create new connections as high traffic will come. RDS proxy will use data base connection pooling if lot of connections are open and then as per 
   usage will reuse them instead creating new one. RDS Proxy manages the connection pooling, security , high availability.
5. run IEM to handle high traffic - to explore



**Lambda Autoscaling**
----------------------
Concurrency is the number of in-flight requests that your AWS Lambda function is handling at the same time. 
For each concurrent request, Lambda provisions a separate instance of your execution environment. As your functions receive more requests, 
Lambda automatically handles scaling the number of execution environments until you reach your account's concurrency limit.

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

    **Understanding reserved concurrency and provisioned concurrency**





