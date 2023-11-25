# Architectural Patterns

## Event Driven

https://youtu.be/ogoztX51-Xg - Event-driven Architecture - Everything You Need to Know - Ask Cloud Architech
Point to Point vs Event Router based communications (SNS / SQS)

## Microservices vs Monolithic

https://youtu.be/lL_j7ilk7rc - Microservices Explained in 5 Minutes - 5 Minutes or Less
https://youtu.be/rv4LlmLmVWk - Microservices explained - the What, Why and How? - TechWorld with Nana
eg. Monolithic = Three Tier - Presentation, Logical, Data vs  Microservice = Logic and Data Layer as many APIs using containers and async messaging / http request / service mesh (kubernetes)
Scaling issues is main driver

Three-tier app to microservice/serverless - https://youtu.be/0u9Mk5g-NxY Back to Basics: Running Serverless Websites - AWS

## Choreography vs Orchestration

https://youtu.be/goRhvp0GOhg - AWS On Air ft. Orchestration vs Choreography - AWS Events
Microserices communicate with each other - Trigger Based - Events - EventBridge (Routing Tools, Schema Registry, etc)

vs 

Coordinator - Stepfunctions, MWAA (Apache Airflow)

https://youtu.be/lJxWhKFriOs - # DevOps Orchestration | DevOps Tutorial | DevOps Training Videos | Simplilearn

## Fanout

https://youtu.be/8BEwZnUIZfw - Back to Basics: Building Fan-Out Serverless Architectures Using SNS, SQS and Lambda
Pub/Sub Fanout - SNS (Built in retries and failure handling, filter policy) prefered when multiple subscribers get same message - Example Architecture in the video

# Idempotency

API --> Resiliency - Exponential backoff

https://youtu.be/I08syTslan8 - What is API Idempotency and Why Is It Important? - Be A Better Dev

when request can be retransmitted or retried with no additional side effects (multipe invocations) - request tokens using API Arguments in a data store - client generated token is better - syntactically identical responses

# Differences between stateful and stateless concepts

# Differences between tightly coupled and loosely coupled components

# Fault-tolerant design patterns (for example, retries with exponential backoff and jitter, dead-letter queues)

## Retries, Exponential Backoff and Jitter (and Timeouts, Graceful Degredation, Circuit Breaker)

https://youtu.be/CDX7oQkuf3A - AWS Developer Webinar Series: Five design patterns to build more resilient applications | AWS Events

Timeouts, polly (.Net),  fallback

## Dead-letter queues

## Circuit Breaker Pattern

https://youtu.be/ADHcBxEXvFA - Circuit Breaker Pattern - Fault Tolerant Microservices - Defog Tech

Types of failures - immediate, timeout

## Bulkhead

https://youtu.be/R2FT5edyKOg - Bulkhead Pattern - Fault Tolerant Microservices - Defog Tech

# Differences between synchronous and asynchronous patterns

https://youtu.be/6XTGcgt5clQ - # How Microservices Communicate? Sync vs Async. Direct vs Brokers And Event Busses - DevOps Toolkit

Wait for response eg. HTTP Rest vs Dont wait as there is a broker (events) AMQP, MQTT or multiple recievers eg. Kubernetes controllers
