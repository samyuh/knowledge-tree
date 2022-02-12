---
---

# Message Oriented Middleware (MOM)
It is not always the case that a user is online to receive a message from another machine. A solution for this case is to use Message Oriented Middleware (MOM), where the messages are stored in a **middleware** as long as needed to deliver the message.

There’re mainly two flavors of MOM:
→ Peer to Peer
→ Publisher/Subscriber

### Peer to Peer
The peer to peer approach contains one queue, where the sender**s** stores the messages in this queue and the receivers, when online, pop the information from that queue, but once the data is popped from the queue, other clients will not receive it.

### Publisher/Subscriber
We can have many publishers and many subscribers. By publishing a message, the information **replicated** and **stored** in the queues of each subscribers that subscribed for that topic. Thus, all the subscribers of a certain topic will read the same information independently of one another.

Normally the [[Asynchronous]] *Communication* between sender and receiver is used when these are **loosely coupled.**