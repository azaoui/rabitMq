## Introduction to RabitMQ:
Based on : https://www.cloudamqp.com/blogs

#### What is RabitMQ:

RabitMQ is a messaging-queuing also known as a message broker or queue manager, it is a software where where queues are defined, to which
applications connect in order to transfer messages

<img src="docs/message-queue-small.png" width="300" height="200">

A message can include any of information to start other process or application or it could be a sample text message.
The queue software stores the messages until a recieving application connects and consume messages from the queue and process them.

#### Real case  RabitMQ: 

A message broker acts as a midleman for various services, it can be used to reduce loads and delivery times of web application servers by delegating tasks that take a lot of time or ressources to a third party that has no other job.

##### Senario:

A web application that allows users to upload information to website, the website will handle this information, generate a pdf, and email back to the user, as this task can take several seconds a message queue will be used to perform the task.
When the use has entred user information into the web information, the web application will create a "PDF processing" message that includes all of the imprtant information the user needs into a messafe and place it into a queue defined in RabbitMQ.

<img src="docs/workflow-rabbitmq.png">

The basic architecure of a message is simple- there are client applications callaed producers that crate messages and deliver them to a broker (the message queue).Other applications, called consumers, connect to the queue and subscibe to the messages to be processed.
A software may act as a producer or consumer or both of them.
Messages placed onto queue are stored until the consumer retrieves them.

#### When and why should use RabitMQ:

When you want to quickly respond requests instead of being forced to perform heavy procedures that may delay response time.
It can used also when you whant to distribute to multiple consumers or to balance loads between workers.

#### Pros:

Producing and consuming messages at the same time (The consumer takes a message off the queue and starts processing the PDF. At the same time, the producer is queueing up new messages. )

The request can be createdin one programming language and handled in another programing language.
Low coupling between the two apllication, they will only communicate through the messagesing they are sending to each other.

<img src="docs/rabbitmq-beginners-updated.png">

The user sends a PDF creation request to the web application.
The web application (the producer) sends a message to rabitMQ that includes data from the request such as name and email.
An exchange accepts the message from the producer and routes them to correct message queues form PDF creation.
The PDF processing worker (the consumer) recieves the task message and start processing the PDF.


#### EXCHANGES :

Messages are not published directly to a queue; instead, the producer sends messages to an exchange.
An exchnage is reponsible for routing the message to different queues with the help of bindings and routing keys.
A binding is a link beween a quee and exchange.

#### Message flow in RabbitMQ :

<img src="docs/exchanges-bidings-routing-keys.png">

1. The producer publish message to an exchange(the exchange type must be specified)
2. The exchange recieve the message and its now reponsible for routing the message(the exchange take different message attributes into account such as the routing key, depending to the exchange type.)
3. Binding must be created from the exchange to queues.(in the schema there is 2 bindings to 2 different queue)
4. The exchange routes the message into the queues depending in message attribute.
5. The messages stay in the queue unti they are handled by a consumer.
6. The consumer handlers the message.





