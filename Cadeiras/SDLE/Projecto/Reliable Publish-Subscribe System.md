# Project
## 1. Introduction
In this project, you shall design and implement a reliable publish-subscribe service.

## 2. Specification
Essentially, this service offers two simple operations:
`put()` - to publish a message on a topic
`get()` - to consume a message from a topic

Messages are arbitrary byte sequences.
In addition, you should provide the operations:

`subscribe()` - to subscribe a topic

`unsubscribe()` - to unsubscribe a topic

Topics are identified by an arbitrary string.
Topics are created implicitly either when a publisher publishes to a topic that does not exist yet, or when a subscriber subscribes to a topic that does not exist yet.
All subscriptions are **durable**, according to the Java Message Service's terminology. I.e. a topics subscriber should get all messages put on a topic, as long as it calls `get()` enough times, until it explicitly unsubscribes the topic, even if it may run intermittently.

###### - Exactly-once
This publish-subscribe service should guarantee "exactly-once" delivery, in the presence of communication failures or process crashes, except in "extreme circumstances", which should be as few as possible, i.e. only rarely and only under some failure conditions. Note that processes may crash and recover, and processes may be unreachable for some time, but eventually the network heals.
By "exactly-once" delivery guarantees we mean the following: 
1.  on successful return of `put()` on a topic, the service guarantees that the message will eventually be delivered "to all subscribers of that topic", as long as the subscribers keep calling `get()`
2.  on successful return from `get()` on a topic, the service guarantees that the same message will not be returned again on a later call to `get()` by that subscriber

###### Solution: [https://zguide.zeromq.org/docs/chapter5/#Getting-an-Out-of-Band-Snapshot](https://zguide.zeromq.org/docs/chapter5/#Getting-an-Out-of-Band-Snapshot "https://zguide.zeromq.org/docs/chapter5/#Getting-an-Out-of-Band-Snapshot")

In order to be able to satisfy these requirements subscribers must have an id, which can be an arbitrary string.

Concurrent invocations of `put()` and `subscribe()/unsubscribe()` make it hard to define "all subscribers of that topic" in the first guarantee. We will not try to specify rigorously what these subscribers should be. However, the idea is that in a single server implementation of the service, if the server has successfully processed a subscription request by a subscriber before it processes a put request by a publisher, and afterwards that subscriber calls `get()` enough times and does not unsubscribe that topic, one of the `get()` calls will return the message published as an argument of that `put()`.

## 3. Constraints
Your service must be implemented on top of libzmq, a minimalist message oriented library. You can use any language for which libzmq has a binding.
This project must be carried out in groups of 4, exceptionally 3 students. (So as to ensure that in each section, there are no groups with more than 4 students, or less than 3 students.)

### 4. What and how to submit?
By November 26, at 20:00, you must submit your code and a plain ASCII file named `README` with instructions for compiling and running your application via [FEUP's Git Service](https://git.fe.up.pt/) (on a project we will create and assign you).

Furthermore, you must submit a report, a PDF file, also via Gitlab@FEUP. The report shall cover the design as well implementation aspects, and possible tradeoffs, with a focus on the algorithms you designed to ensure the "exactly-once" guarantees above under the failure model described above.

## More Info
The project's implementation must include a service and test clients that will allow you to test the service.  
The test clients should use a "library" that allows them to access the service. This client-side library together with the service implementation is what JMS calls the "provider".  
The main task of the project is to implement a provider that satisfies the requirements in the project specification.  
The clients are as I mentioned just for test/demo purposes. (You can use one client playing the role of a publisher and another the role of a subscriber, or you can use a single client that can play both roles.) The design of these clients, like that of the provider, is up to you. However, you should strive to make it possible to easily automate tests. In my opinion, requiring interactive input from a user is not the best way to achieve that goal.

Persistente -> Once and only only once, not missed even if the client is inactive