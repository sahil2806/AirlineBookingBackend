--> clone the project on your local Execute npm install on the same path as of your root directory of teh downloaded project Create a .env file in the root directory and add the following environment variable PORT=3000 Inside the src/config folder create a new file config.json and then add the following piece of json { "development": { "username": <YOUR_DB_LOGIN_NAME>, "password": <YOUR_DB_PASSWORD>, "database": "Flights_Search_DB_DEV", "host": "127.0.0.1", "dialect": "mysql" } }

Once you've added your db config as listed above, go to the src folder from your terminal and execute npx sequelize db:create and then execute npx sequelize db:migrate

                             ---Airline Back-end System----

Objective
We need to build a back-end system that can support different features for an airline company. Our end user is going to be someone who wants book flight and query flight so we need a robust system to actually help them give the best experience possible .This doc is solely going to focus on the back-end part of the system.We want to prepare the whole back-end keeping  the fact in Mind that the code base should be as maintainable as possible.

Requirement
-- A user should be able to search for flight from one place to another
- user should be able to mention the source and destination.
- user should be able select the data of the journey.
       -[v2] user should be able to search for return flight and multi city flight 
- user should be able select the class of the flight[Not mandatory].
- user should be able select the no of seats they want to book.
[Not mandatory].
- Now based on the above data . we will list down the flight.
-we should show our users the best available flight at the top .Based on time period of flight and then based on the price.
-we need to support pagination so that we can list  down.Some chunk of flight at  point of time.
- we should support filters of flights based on the price ,departure 
 Time,  Duration time, Airline.
        - v[2] we can add support for more filters
-- A user should be able to book a flight considering that user is registered on the platform. 
-- Users should be able to cancel a booking and then based on the Some criteria we can initiate a refund for them.
-- User should be able to request and book excess luggage for every flight .
-- Tracking flight should be possible , the user should be notified about Any price drops or any delays.
-- user should be able to list their previous and upcoming flight.
-- user should be able to download their boarding pass if they have done online check-in.
-- online check - in mechanism should be supported.
-- Notification via email for completing online check-in before 3 hours of departure.
--Notification to the user about any flight delay.
-- Users should be able to review the flight journey if and only if they have booked the flight.
        -- Review mechanism should involve star rating along with comment.
        --  While listing the flight details we should also display the review of flight.
-- User should be able to authenticate to our system using email and 
       Password.
      - [v2] support ticketing , where users can raise their queries.   
 --  Listing FAQ which  will be static data.
      - [v2] prepare seat selection.
-- Coupons an discounts and offers.
-- while making a booking a person can reserve more than one seat With one login id.


Non Functional Requirement:
- We can expect that we are going to have more flight searches than 
flight booking.
-  The system needs to be accurate in terms of booking.
- Expect that we will be having approx 1,00,000 total users, 5,00,000 Booking might come up in one quarter.
- So in one day we can expect 5000 bookings.
- System should be  capable of scaling up to 3x current estimated traffic
-The system should be handled real time update to flight prices , before The user make the final booking.
- Concurrency should be handled using RDBMS be the the good solution.



Capacity Estimation:

-  Storage Estimates - 
        - For upcoming 5 years 80,00,000 booking , 2,00,000 users, Considering all the users record and user ]booking record Take 10MB of data, then overall  10 TB of memory should Be fine for our initial pilot 
          run.
-  Traffic estimate - If  we consider 30:1 as the search : booking ration  hen at max we expect 1,50,000 search queries a day 2query/s.



![Alt text](/image/RabbitMQimage.png)


1. Message Ordering
RabbitMQ: Guarantees message order only in single-consumer setups. In multi-consumer environments, messages can be processed out of order since RabbitMQ distributes messages across consumers to balance the load. If messages are requeued (e.g., due to failures), the original order may also be disrupted.
Kafka: Provides strict ordering within each partition. When a topic is divided into partitions, Kafka preserves the order of messages within each partition. Multiple consumers can read from different partitions without disrupting order, which makes Kafka ideal for applications where event sequence matters.
2. Message Retention and Replayability
RabbitMQ: Primarily designed for real-time message delivery, RabbitMQ doesn’t retain messages once they are consumed. It focuses on transient messaging, where messages are processed and then discarded. While RabbitMQ can be configured to store unprocessed messages, it lacks Kafka’s log-based approach to durable storage.
Kafka: Kafka is built to store messages durably for a configurable time (days, months, or indefinitely). This makes Kafka ideal for applications that need to replay or reprocess messages, such as event sourcing, audit logging, and data pipelines.
3. Architecture and Use Case Focus
RabbitMQ: Functions as a traditional message broker using a push-based model where messages are routed and delivered directly to consumers in real-time. Its design includes rich routing capabilities, such as fan-out, direct, and topic exchanges, which makes it ideal for task queues, notifications, and real-time message delivery.
Kafka: Kafka’s log-based architecture is optimized for high-throughput, distributed streaming, and event logging. Kafka uses a pull-based model where consumers pull data at their own pace, making it well-suited for data streaming, log aggregation, and real-time analytics on large data volumes.
4. Scalability and Throughput
RabbitMQ: Scales well for smaller to moderate workloads with low latency. It’s designed to handle lower message volumes and is more commonly used in smaller systems or real-time applications that need fast, transient message processing. However, it may struggle with extremely high-throughput scenarios.
Kafka: Designed for high scalability and can handle millions of messages per second with very low latency across large, distributed systems. Kafka’s partitioned architecture allows it to scale horizontally by adding more partitions and nodes, making it ideal for applications needing massive data processing.
5. Message Delivery Acknowledgment and Reliability
RabbitMQ: Allows for flexible acknowledgment options. Messages can be acknowledged after being successfully processed, and unacknowledged messages can be requeued if there’s a failure. However, requeued messages may disrupt the original order, which can impact reliability in ordered processing.
Kafka: Uses a commit log approach where each message offset is tracked by the consumer. Kafka stores uncommitted messages durably, and consumers can restart from their last committed offset to resume message processing reliably. This is particularly useful for fault tolerance and maintaining state in event-driven systems.
Summary of Key Differences:
Ordering: RabbitMQ has limited ordering guarantees; Kafka enforces strict ordering within partitions.
Retention: RabbitMQ discards messages after consumption; Kafka retains messages for configurable durations.
Architecture: RabbitMQ uses push-based, real-time delivery; Kafka is pull-based, optimized for data streaming.
Scalability: RabbitMQ handles lower-throughput applications; Kafka excels at high-throughput, large-scale applications.
Reliability: RabbitMQ requeues unacknowledged messages but may disrupt order; Kafka uses offset tracking for reliable, fault-tolerant processing.



authService API

![Alt text](/image/Picture1.png)

FlightAndSearchServcie API

![Alt text](/image/Picture2.png)

BookingService API

![Alt text](/image/Picture3.png)

ReminderService API


![Alt text](/image/Picture4.png)

