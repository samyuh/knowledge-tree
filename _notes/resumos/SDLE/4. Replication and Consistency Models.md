# Data replication

The data replication allow us to have:

-   **Reliability:** since the data cannot be lost, unless the data is lost in all replicas
-   **Availability:** the data is always available, unless the all the replicas are offline.
-   **Scalability:** we can have a balance load across nodes

The challenge is to have consistency between replicas.

![[Data replication scheme.png]]

# Strong consistency

[Eventual Consistency vs Strong Consistency](https://medium.com/system-design-blog/eventual-consistency-vs-strong-consistency-b4de1f92534d)

“Simply put, data has to be locked during the period of update or replication process to ensure that no other processes are updating the same data.”

It has deterministic updates: **same initial state** leads to **same result.**

# Sequential consistency model

[Sequential consistency in newbie terms?](https://stackoverflow.com/questions/54493739/sequential-consistency-in-newbie-terms)

The operations executed by any thread (in any processor) appear in the order they are executed, in order words, in a sequential order.

## Linearizable

Charron-Bost, Bernadette, Fernando Pedone, and André Schiper, eds. _Replication: Theory and Practice_. Vol. 5959. Lecture Notes in Computer Science. Berlin, Heidelberg: Springer Berlin Heidelberg, 2010. [](https://doi.org/10.1007/978-3-642-11294-2)[https://doi.org/10.1007/978-3-642-11294-2](https://doi.org/10.1007/978-3-642-11294-2). [chap 1.3]

We can say that an execution _E_ is linearizable if **there is a sequence** the obeys the following rules:

[L1] The linear sequence H contains all the operations E has, each paired wit the return value received in E. 
**[L2]** **the real-time total order of operations in H is compatible with the partial order**
[L3] H is a legal history of the sequential data type that is replicated.

Now consider that following sequence:

![[Consistency 1.png]]

We have that the _write(1)_ occurs before _write(2), read(2), snapshot() and write(3)._ Also, _read(1)_ occurs before _write(2), read(2), snapshot and write(3). read(2)_ occurs before _snapshot()._

Thus a candidate for a linear order is:

write1, read1, read2, write2, snapshot and write3.

This order obeys the rules [L1], [L2] and [L3].

This system below, however, is **not** linearizable, because at this time the _write_ operation might returns before the replicas were actually modified. Thus, there’s no guarantee of the linearizability:

![[Consistency(2).png]]

Notice that in real-time partial order **write(3)** must be before snapshot(), **because it returns before**. But the result returned by snapshot() is not compatible with this order. In other words, write(3) took place before snapshot(), but the effects were just visible after the snapshot().

### TIPS!

[Princeton](https://www.cs.princeton.edu/courses/archive/fall19/cos418/docs/precept8_consistency.pdf)

1.  A completed write appears to all future reads.
2.  Once a read sees a new value, all future reads reads must return the new value
    

## Sequential consistency

[Sequential Consistency](https://jepsen.io/consistency/models/sequential)

> Informally, sequential consistency implies that operations appear to take place in some total order, and that that order is consistent with the order of operations on each individual process.

In fact the system above is not linearizable, but it has sequential consistency. Consider $<_{E, rc}$ is the client partial order symbol used. Then, we can say in $p <_{E, rc}q$, **p** and **q** occur in the same client and cronologically **p** returns before **q.**

The rules to a system have sequential consistency are similar to a system that is linearizable. We can say that there’s a sequential consistency if there’s a sequence of the system that obeys:

[L1] H has the same operations of E, each paired with the return value received in E
[L2] **H obeys the client partial order**
[L3] H is a legal history of the sequential data type that is replicated

The client partial order is a weaker version of the standard partial order. Thus a **every linearizable system also has sequential consistency.**

Since the client partial-order just points that there’s an order in the same client, it’s ok to place the snapshot before the write(3).

### Sequential Consistency does not Compose

We may have two systems that are sequential consistent in separate (U and T), but the composition of partial sequential consistency systems, we not always have a sequential consistent system.

![[Consistency(3).png]]

This execution is not sequentially consistent.

The sequence must be:

-   **T:** write(2,7) write(0,8) snapshot0,1() [0→8, 1→0]
-   **U:** write(1,5) write(3,2) snapshot2,3() [2→0, 3→2]

The snapshots tells us that:

-   write(0) $<_{e,ct}$snapshot0,1$<_{e,ct}$write(1)
-   write(3) $<_{e,ct}$snapshot2,3$<_{e,ct}$write(2)

The relation with the client partial order does not hold. Because

write(2)$<_{e,ct}$write(0)$<_{e,ct}$write(1), but write(3) is after write(1) and before write(2).

> If we were able to merge it into just one timeline and this timeline H obeys the client partial order, then this would be sequential consistent.

In the following example: We can say that the order might be:

-   write(1)
-   read(1)
-   read(2)
-   write(2)
-   snapshot()
-   write(3) And this order obeys the client partial order.

![[Consistency(4).png]]

## One-copy serializability (transaction-based system)

-   The execution of a set of transaction has the same result as if it was executed in a single processor.
-   It’s like we have a total order, all operations are transactions and provides isolation
-   Nowadays the systems provide weaker consistency to improve performance