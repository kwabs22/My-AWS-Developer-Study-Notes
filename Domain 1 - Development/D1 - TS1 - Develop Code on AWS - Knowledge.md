# Architectural Patterns

## Event Driven

https://youtu.be/ogoztX51-Xg - Event-driven Architecture - Everything You Need to Know - Ask Cloud Architech
Point to Point vs Event Router based communications (SNS / SQS)

## Microservices vs Monolithic

https://youtu.be/lL_j7ilk7rc - Microservices Explained in 5 Minutes - 5 Minutes or Less
https://youtu.be/rv4LlmLmVWk - Microservices explained - the What, Why and How? - TechWorld with Nana
eg. Monolithic = Three Tier - Presentation, Logical, Data vs  Microservice = Logic and Data Layer as many APIs using containers and async messaging / http request / service mesh (kubernetes)
Scaling issues is main driver

Three

## Choreography vs Orchestration

https://youtu.be/goRhvp0GOhg - AWS On Air ft. Orchestration vs Choreography - AWS Events
Microserices communicate with each other - Trigger Based - Events - EventBridge (Routing Tools, Schema Registry, etc)

vs 

Coordinator - Stepfunctions, MWAA (Apache Airflow)

## Fanout

https://youtu.be/8BEwZnUIZfw - Back to Basics: Building Fan-Out Serverless Architectures Using SNS, SQS and Lambda
Pub/Sub Fanout - SNS (Built in retries and failure handling, filter policy) prefered when multiple subscribers get same message - Example Architecture in the video

# Idempotency


# Differences between stateful and stateless concepts


# Differences between tightly coupled and loosely coupled components


# Fault-tolerant design patterns (for example, retries with exponential backoff and jitter, dead-letter queues)



# Differences between synchronous and asynchronous patterns
