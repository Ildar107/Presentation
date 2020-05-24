1. 

Hi every one! My name is Ildar. Today we are gonna talk about RabbitMQ.

2.

RabbitMQ is a message-queueing software also known as a message broker or queue manager.

Message-broker is an intermediary computer program module that translates a message from the formal messaging protocol of the sender to the formal messaging protocol of the reciver.

3. 
Why do we need to use a message-broker?
Imagine you have your own application. For example, it's an online store.
So, you permamently work in your technological scope, and one day you need to make the application interact with another one. 
In previous times, you would use simple "in points" of the machine to machine communication. But nowdays we have special message brokers.
They make the process of data exchange simple and reliable. These tools use different protocols that determine the message format.
The protocols show how the message should be transmitted, processed, and consumed. By the way RabbitMQ implements AMQP protocol version 1.0 and 0-9.

4. 

Now we know why we need to use message-broker, but now we need to know when to use it.

1) If you want to control data feeds. For example, the number of registrations in any system.

2) When the task  is to put data to several applications and avoid direct usage of their API.

3) The necessity to complete processes in a defined order like a transaction system.

5.

Ok, what does the RabbitMQ structure look like?
How you can see in the diagram below RabbitMQ have a several main parts.
The main parts include the following blocks:

1) Producer is an application that sends messages.

5.1

2) Exchange receives messages from producers and pushes them to queues depending on rules defined by the exchange type. To receive message, queue needs to be bound to at least one exchange.

    RabbitMQ has 3 suitable message exchange model:
    
    a) Direct exchange model (individual exchange of topic one be one)
    b) Topic exchange model (each consumer gets a message which is sent to a specific topic)
    c) Fanout exchange model (all consumers connected to queues get the message).

    Also exchange has 2 important parameter like routing key and binding. 
    Rouating key is a key that the exchange looks at to decide how to route the message to queues.
    Think of the routing key like an address for the message.
    A binding is a link between a queue and an exchange.

3) Message queue is a buffer that stores messages

4) Consumer is a client application that requests messages from a message queue.


5.2

Now we have know all the main parts of RabbitMQ and let's find out how it all works.

1) Step one. The producer publishes a message to an exchange. When creating an exchange, the type must be specified.

2) Step two. The exchange receives the message and is now responsible for routing the message. 
The exchange takes different message attributes into account, such as the routing key, depending on the exchange type.

3) Step three. Bindings must be created from the exchange to queues. In this case, there are two bindings to two different queues from the exchange. 
The exchange routes the message into the queues depending on message attributes.

4) Step four. The messages stay in the queue until they are handled by a consumer.

5) Step five. The consumer handles the message.

6. 

Let's make one simple "Hello World" example

First install amnqp module.

6.1
In the sender part we need to requiere the library first. Then connect to RabbitMQ server.
Next we create a channel, which is where most of the API for getting things done resides.
To send, we must declare a queue for us to send to; then we can publish a message to the queue.
The message content is a byte array, so you can encode whatever you like there.
Lastly, we close the connection and exit.


6.2
That's it for our sending part. Our recieving part listens for messages from RabbitMQ, so unlike the sending part which publishes a single message, 
we'll keep the recieving part running to listen for messages and print them out.

Setting up is the same as the sending part; we open a connection and a channel, and declare the queue from which we're going to consume. 
Note this matches up with the queue that sendToQueue publishes to.
We're about to tell the server to deliver us the messages from the queue. 
Since it will push us messages asynchronously, we provide a callback that will be executed when RabbitMQ pushes messages to our consumer. 
This is what Channel.consume does.

7. 

Now we can run both scripts. In a terminal, from the project folder, run the publisher.

Then, run the consumer.

The consumer will print the message it gets from the publisher via RabbitMQ. The consumer will keep running, waiting for messages.

8. 

Finally RabbitMQ has a large number of clients in different languages, its code is also completely open, as it is an open source project. That's why you should use it.
