# Threads

Threads may share many resources, but they do not share the stack, which makes sense, since it would avoid two functions be running in parallel.

## User level threads

The kernel is not aware of these threads. The thread library must provide functions such as create/destroy threads, thread synchronization, the library is responsible for keeping the thread table.

**Problems:** there’re two main problems with the user level threads. One we cannot exploit the use of **multiprocessors** and when there’s a page-fault the single kernel thread is put to **WAIT**, thus the other user level threads also stops.

## Kernel level threads

The **kernel** schedules a core for the thread and the operational system keeps a **threads table** with the information of every thread. This type of operation includes a System Call.

## Hybrid implementation (m:n)

This implementation maps the user level threads to kernel-threads. On this way the number of user level threads increases.

## Thread pool

-   [+] Limits the maximum number of threads
-   [-] May cause an overhead for switching. You may want to use semaphores.
-   [+] Avoid the overhead of destroying and creating threads.

# Multi-threaded Server

This is what was implemented in SDIS. We have one server, one dispatcher to receive the messages and allocates workers (threads) to handle the processing. When a worker finishes its job, it sends the information back to the network.

# Event Driven Server

The operations are scheduled using non-blocking IO operations. It needs to keep a FSM for each request event.