# Application Integration

## SQS Simple Queue Service
Amazon SQS is a web service that gives you access to a message queue that can be used to store messages while waiting for a computer to process them. Amazon SQS is a distributed queue system that enables web service applications to quickly and reliably queue messages that one component in the application generates to be consumed by another component. A queue is a temporary repository for messages that are awaiting processing.

Using SQS you can decouple the components of an application so they run independently, easing message management between components. Any component of a distributed application can store messages in a fail-safe queue. Messages can contain up to 256 KB of text in any format. Any component can later retrieve the message programmatically using Amazon SQS API.

The queue acts as a buffer between the component producing and saving data, and the component receiving the data for processing. This means the queue resolves issues that arise if the producer is producing work faster than the consumer can process it, or if the producer or consumer are only intermittently connected to the network.

- SQS is pull based, not pushed based
- Messages are 256 KB in size by default, you can go up to 2GB using S3 for more cost
- Messages can be kept in queue for 1 minute to 14 days. The default retention is 4 days.
- Visibility Time Out is the amount of time that the message is invisible in the SQS queue after a reader picks up that message. Provided the job is processed before the visibility time out expires, the message will be deleted from the queue. If the job is not processed within that time, the message will become visible again and another reader will process it. This could result in the same message being delivered twice.
- Visibility Time Out Maximim is 12 hours
- SQS guarantees that your messages will be processed at least once
- Amazon SQS long polling is a way to retrieve messages from your Amazon SQS queues. While the regular short polling returns immediately (even if the message queue being polled is empty), long polling doesn't return a response until a message arrives in the message queue, or the long poll times out.
- Long polling can be a option to save money if it meets your SQS needs

### Types of queues in SQS
- #### Standard Queues (default)
    Amazon SQS offers standard as the default queue type. A standard queue lets you have nearly unlimited number of transactions per second. Standard queues guarentee that a message is delivered at least once. However, occasionally (because of the highly distributed architecture that allows high throughput), more than one copy of a message might be delivered out of order. Standard queues provide best effort ordering which ensures that messages are generally delivered in the same order they are sent.

- #### FIFO Queues
    The FIFO queue complements the Standard Queue. The most important features of this queue type are FIFO (first in first out) delivery and exactly once processing: The order in which messages are sent and recieved is strictly preserved and a message is delivered once and remains available until a consumer processes and deletes it; duplicates are not introduced into the queue.
 
    FIFO queues also support message groups that allow multiple ordered message groups within a single queue. FIFO queries are limited to 300 transactions per second (TPS), but have all the capabilities of standard queues.
 
 ## SWF (Simple Workflow Service)
Amazon Simple Workflow Service Service (SWF) is a web service that makes it easy to coordinate work across distributed application components. SWF enables applications for a range of use cases, including media processing, web application backends, business process workflows, and analytics pipelines, to be designed as a coordination of tasks.

Tasks represent invocations of various processing steps in an application which can be performed by executable code, web service calls, human actions, and scripts.

- A way to combine your digital environment along with manual tasks carried out by humans.

### SWF Actors
- #### Workflow Starters
    An application that can initiate (start) a workflow. Could be your e-commerce website following the placement of an order, or a mobile app searching for bus times.

- ### Deciders
    Control the flow of activity tasks in a workflow execution. If something has finished (or failed) in a workflow, a Decider decides what to do next.

- ### Activity Workers
    Carry out the activity tasks

### SWF vs SQS
- SQS has a retention period of up to 14 days. SWF workflow executions can last up to 1 year.
- Amazon SWF presents a task-oriented API, whereas Amazon SQS offers a message-oriented API
- Amazon SWF ensures that a task is assigned only once and is never duplicated. With Amazon SQS you need to handle duplicated messages and may also need to ensure that a message is processed only once.
- SWF keeps track of all the tasks and events in an application. With SQS you need to implement your own application level tracking, especially if your application uses multiple queues.

## SNS (Simple Notification Service)
Amazon Simple Notification Service (SNS) is a web service that makes it easy to set up, operate, and send notifications from the cloud. It provides developers with a highly scalable, flexible, and cost-effective capability to publish messages from an application and immediately deliver them to subscribers or other applications.

SNS supports push notifications to Apple, Google, Fire OS, and Windows devices, as well as Android devices in China with Baidu Cloud Push.

Besides pushing cloud notifications directly to mobile devices, SQS can alos deliver notifications by SMS text message or email to Amazon SQS queues, or to any HTTP endpoint.

SNS allows you to group multiple recipients using topics. A topic is an "access point" for allowing recipients to dynamically subscribe for identical copies of the same notification.

One topic can support deliveries to multiple endpoint types - for example you can group together iOS, Android, and SMS recipients. When you publish once to a topic, SNS delivers appropriately formatted copies of your message to each subscriber.

To prevent messages from being lost, all messages published to Amazon SNS are stored redundantly across multiple availability zones.

### SNS Benefits
- Instanteous push based delivery (no pulling)
- Simple API and easy integration with applications
- Flexible message delivery over multiple transport protocols
- Inexpensive, pay as you go model with no up front costs
- Web based AWS Management Console offers the simplicity of a point and click interface

### SNS vs SQS
- Both messaging services in AWS
- SNS is push based where as SQS is pull based

## Application Integration Review

1. What Amazon service can be used to decouple your infrastructure?

<details>
<summary>Show answer</summary>
<p>
SQS

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sqs-simple-queue-service)
</p>
</details>

2. Is SQS pull based or Push based?

<details>
<summary>Show answer</summary>
<p>
Pull based

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sqs-simple-queue-service)
</p>
</details>

3. What is the default size for SQS messages?

<details>
<summary>Show answer</summary>
<p>
256 KB

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sqs-simple-queue-service)
</p>
</details>


4. What is the time range that messges can be retained in SQS?

<details>
<summary>Show answer</summary>
<p>
1 minute to 14 days

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sqs-simple-queue-service)
</p>
</details>

5. What are the kinds of SQS?

<details>
<summary>Show answer</summary>
<p>

- Standard SQS
- FIFO SQS

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#types-of-queues-in-sqs)
</p>
</details>

6. What is the differnces between Standard SQS and FIFO SQS?

<details>
<summary>Show answer</summary>
<p>

- Standard SQS - Order is not guaranteed and messages can be delivered more than once.
- FIFO SQS - Order is strictly maintained and messages are delivered only once.

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#types-of-queues-in-sqs)
</p>
</details>

7. What is the SQS Visibility Timeout?

<details>
<summary>Show answer</summary>
<p>
Visibility Time Out is the amount of time that the message is invisible in the SQS queue after a reader picks up that message. Provided the job is processed before the visibility time out expires, the message will be deleted from the queue. If the job is not processed within that time, the message will become visible again and another reader will process it. This could result in the same message being delivered twice.

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sqs-simple-queue-service)
</p>
</details>

8. What is the timeout maximum for SQS?

<details>
<summary>Show answer</summary>
<p>
12 hours

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sqs-simple-queue-service)
</p>
</details>

9. Is it guaranteed that with SQS your messages will be processed at least once?

<details>
<summary>Show answer</summary>
<p>
Yes

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sqs-simple-queue-service)
</p>
</details>

10. What is SQS Long Polling?

<details>
<summary>Show answer</summary>
<p>
Amazon SQS long polling is a way to retrieve messages from your Amazon SQS queues. While the regular short polling returns immediately (even if the message queue being polled is empty), long polling doesn't return a response until a message arrives in the message queue, or the long poll times out.

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sqs-simple-queue-service)
</p>
</details>

11. What is the maximum retention period for SQS and SWF?

<details>
<summary>Show answer</summary>
<p>

- SQS maximum retention is 14 days
- SWF maximum workflow execution is 1 year

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#swf-vs-sqs)
</p>
</details>

12. How is the SWF API oriented?

<details>
<summary>Show answer</summary>
<p>
SWF is a task-oriented API

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#swf-vs-sqs)
</p>
</details>

13. How is the SQS API oriented?

<details>
<summary>Show answer</summary>
<p>
SWF is a message-oriented API

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#swf-vs-sqs)
</p>
</details>

14. True or false, SWF ensures that a task is assigned only once and is never duplicated.

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#swf-vs-sqs)
</p>
</details>

15. True or false, with Standard SQS you need to handle duplicated messages and may also need to ensure that a message is processed only once.

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#swf-vs-sqs)
</p>
</details>

16. True or false, SWF keeps track of all the tasks and events in an application.

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#swf-vs-sqs)
</p>
</details>


17. True or false, SQS you need to implement your own application level tracking especially if your application uses multiple queues.

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#swf-vs-sqs)
</p>
</details>

18. What are the different types of SWF Actors?

<details>
<summary>Show answer</summary>
<p>

- Workflow Starters - A application that can start a workflow. Could be your e-commerce wensite following the placement of an order, or a mobile app searching for bus lines.
- Deciders - Control the flow of activity tasks in a workflo execution. If something has finished or failed in a workflow a Decider decides what to do next.
- Activity Workers - Carry out the activity tasks

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#swf-actors)
</p>
</details>

19. True or false, SWF is an instantaneous push based delivery (no polling).

<details>
<summary>Show answer</summary>
<p>
False, SQS is an instantaneous push based delivery (no polling)

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sns-benefits)
</p>
</details>

20. True or false, SQS supports only HTTP protocol.

<details>
<summary>Show answer</summary>
<p>
False, SQS supports multiple transport protocols.

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sns-benefits)
</p>
</details>

21. True or false, SQS is pay as you go with no upfront costs?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sns-benefits)
</p>
</details>

22. True or false, both SNS and SQS are messaging services in AWS.

<details>
<summary>Show answer</summary>
<p>


[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sns-vs-sqs)
</p>
</details>

23. True or false, SNS is pull based.

<details>
<summary>Show answer</summary>
<p>
False, SNS is push based

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sns-vs-sqs)
</p>
</details>

24. True or false, SNS offers a web based AWS Management Console for point and click interface.

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/application-integration.md#sns-benefits)
</p>
</details>

25. What is the difference between SNS and SQS?
- a. SNS sends messages to people on topics, whereas SNS manages tasks
- b. SNS pulls (polls), whereas SQS is push based message service
- c. SQS and SNS are basically the same service
- d. SNS is a push notification service, whereas SQS is message system that requires worker nodes to poll a queue

<details>
<summary>Show answer</summary>
<p>
- d. SNS is a push notification service, whereas SQS is message system that requires worker nodes to poll a queue

SNS is a notification service for sending text based communication of different types to different destinations. SQS is a queue system for asynchronously manages tasks (called messages).
</p>
</details>

2. Amazon SWF is designed to help users ________.
- a. Manage user identification and authorization
- b. Coordinate synchronous and asynchronous tasks
- c. Secure their VPCs
- d. Sotre file based objects

<details>
<summary>Show answer</summary>
<p>
- b. Coordinate synchronous and asynchronous tasks

Similar to SQS, SWF manages queues of work, however unlike SQS it can have out-of-band parallel and sequential task to be completed by humans and non AWS services.
</p>
</details>

3. Amazon SWF restricts me to the use of specific programming languages.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- b. False

While there are a limited range of SDKs available for SWF, AWS provides an HTTP based API which allows you to interact using any language as long as you phrase the interactions in HTTP requests.
</p>
</details>

4. Amazon SWF ensures that a task is assigned only once and is never duplicated.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- a. True

One time only completion is a key feature of SWF. At one time this was a key distinction from SQS, however with SQS FiFo queues, this is no longer a distinguishing feature.
</p>
</details>

5. What application service allows you to decouple your infrastructure using messaged based queues?
- a. SNS
- b. SWF
- c. SQS
- d. SES

<details>
<summary>Show answer</summary>
<p>
- c. SQS

In IT the term 'message' can be used in the common sense, or to describe a piece of data of Task in an asynchronous queueing system such as MQseries, RabbitMQ or SQS.
</p>
</details>

6. What happens when you create a topic on Amazon SNS?
- a. The topic will terminate your EC2 instances that aren't identified by tags
- b. Nothing, as topics are specific to SQS
- c. You cannot create a topic on SNS
- d. An Amazon Resource Name is created

<details>
<summary>Show answer</summary>
<p>
- d. An Amazon Resource Name is created
</p>
</details>

7. Amazon's SQS service guarantees a message will be delivered at least once.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- a. True
</p>
</details>

8. In SWF, what does a "domain" refer to?
- a. A specialized security group configuration
- b. A special type of worker instance
- c. The DNS record for the AMazon SWF service
- d. A collection of related workflows

<details>
<summary>Show answer</summary>
<p>
- d. A collection of related workflows
</p>
</details>

9. What does Amazon SWF stand for?
- a. Simple Wireless Forms
- b. Simple Web Forum
- c. Simple Work Flow
- d. Simple Web Flow

<details>
<summary>Show answer</summary>
<p>
- c. Simple Work Flow
</p>
</details>

10. By default, EC2 instances pull SQS messages from a standard SQS queue on a FIFO (first in first out) basis.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- b. False
</p>
</details>

11. What does Amazon SES stand for?
- a. Software Enabled Server
- b. Simple Email Service
- c. Simple Elastic Server
- d. Software Email Solution

<details>
<summary>Show answer</summary>
<p>
- b. Simple Email Service
</p>
</details>
