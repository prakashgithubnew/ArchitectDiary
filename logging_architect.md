**Difference between logging and tracing**
------------------------------------------
logging - Finding any issues or errors in each component
tracing - Tracking the flow of requests as they move through various components and 
          services within a distributed system. it shows how many request failed with what error,
            what was the response time, what was the response code, duration of the whole request,
            successful request, method requested.



Distributed tracing consists of two main concepts

Trace Id(same as correlation id) -is used to trace an incoming request and track it across all the composing services to satisfy a request
Span Id - spans in between service calls to track each request that is received and to the response that is sent out.

Tools and utilities which can be used for distributed logging in microservices
----------------------------------------------------------------------------------------------
Solution 1 - Use elastic search and kibana option
-----------
Elastic Search is one of the best tools for distributed logging on microservices architectures.
Elasticsearch is the preferred full-text search search engine in processes such as content search, 
data analysis, queries and suggestions, especially due to its performance capabilities, powerful and 
flexible features.

<span style="color: green">**Elastic search**</span> 
1. Elasticsearch is a distributed, open source search and analytics engine. If you need security and alert features with Kibana, then it is required to purchase commercial pack.
2. Elasticsearch is an open source database that is well suited for indexing logs and analytical data.
3. It is developed in Java and is based on Apache Lucene
4. Elastic-search has a restful API which brings result for its open source database. 
5. it is scalable and easy to install.
6. Elasticsearch is fast
7. Elastic Search is made with high speed and high availability.

<span style="color: green">**Kibana**</span> 
its a user interface to fetch results from Elastic search
it calls Elastic Search API to fetch results from search engine.


Solution 2 - using spring-cloud-sleuth and spring-cloud-zipkin
--------------------------------------------------------------




**How logging is handled in MAE**
---------------------------------

we have enabled AWS X-Ray. Utility PL runs by devops team who has enabled XRay for each cell. 
we are following below approach in MAE-

**Approach 1** - Using tracing we can get responses,latency , failure , successful call details.
------------------------------------------------------------------------------------------------
1. Added @Tracing(segmentname="") in controller method only, no where else.This is coming from aws sk jar 
    named powertool tracing jar.
2. What ever the segment name is provided in the name the same is tracked in cloud watch logs.
3. Add below in orchestrator file in the start of method which starts a segment 
    AWSXRay.beginSegment("AIP_OTHER_PROPERTY_MORTGAGE_SEGMENT")
    in the end of method
    AWSXRay.endSegment()

This apporach is also good to understand the memory optimizer of lambda.

**Approach 2**
--------------
use log.info,log.debug,log.error which provides 

