# Application Integration

## SQS Simple Queue Service
Amazon SQS is a web service that gives you access to a message queue that can be used to store messages while waiting for a computer to process them. Amazon SQS is a distributed queue system that enables web service applications to quickly and reliably queue messages that one component in the application generates to be consumed by another component. A queue is a temporary repository for messages that are awaiting processing.

Using SQS you can decouple the components of an application so they run independently, easing message management between components. Any component of a distributed application can store messages in a fail-safe queue. Messages can contain up to 256 KB of text in any format. Any component can later retrieve the message programmatically using Amazon SQS API.

The queue acts as a buffer between the component producing and saving data, and the component receiving the data for processing. This means the queue resolves issues that arise if the producer is producing work faster than the consumer can process it, or if the producer or consumer are only intermittently connected to the network.

- SQS is pull based, not pushed based
- Messages are 256 KB in size by default, you can go up to 2GB using S3 for more cost
- Messages can be kept in queue for 1 minute to 14 days. The default retention is 4 days.
- Visibility Time Out is the amount of time that the message is invisible in the SQS queue after a reader picks up that message. Provided the job is processed before the visibility time out expires, the message will be deleted from the queue. If the job is not processed within that time, the message will become visible again and another reader will process it.This could result in the same message being delivered twice.
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

## SQS vs SWF
- SQS has a retention period of up to 14 days. SWF workflow executions can last up to 1 year.
- Amazon SWF presents a task-oriented API, whereas Amazon SQS offers a message-oriented API
- Amazon SWF ensures that a task is assigned only once and is never duplicated. With Amazon SQS you need to handle duplicated messages and may also need to ensure that a message is processed only once.
- SWF keeps track of all the tasks and events in an application. With SQS you need to implement your own application level tracking, especially if your application uses multiple queues.
