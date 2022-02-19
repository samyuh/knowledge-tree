# TCP reliability

TCP is not able to filter duplicated data for this reason we cannot risk to send duplicated information. There’re some applications, for example, that works with **non-indepotent** operations (e.g credit/debit operations).

# RPC

The request is made by the use of a _client stub._ The stub _assembles (**marshall**)_ the parameters and **send** to the server stub. It **blocks** until receives a response (in a sync scenario).

Then the server stub receives the response, parses the message (_**unmarshall**),_ call the function and after the actual function returns the result, the server stub receives it, _**marshalls**_ it and send back to the client stub.

Upon the reception of the result, the client stub _**unmarshalls**_ the response and give it back to the client.

# Asynchronous communication

## Message Oriented Middleware (MOM)

It is not always the case that a user is online to receive a message from another machine. A solution for this case is to use Message Oriented Middleware (MOM), where the messages are stored in a **middleware** _as long as needed_ to deliver the message.

There’re mainly two flavors of MOM:

### Point-to-Point

The point to point approach contains one queue, where the sender**s** stores the messages in this queue and the receivers, when online, pop the information from that queue, but once the data is popped from the queue, other clients will not receive it.

### Publisher/Subscriber

We can have many publishers and many subscribers. By publishing a message, the information **replicated** and **stored** in the queues of each subscribers that subscribed for that topic. Thus, all the subscribers of a certain topic will read the same information independently of one another.

Normally the **Asynchronous Communication** between sender and receiver is used when these are **loosely coupled.**