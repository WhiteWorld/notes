# Time and order

Total and partial order
A total order is a binary relation that defines an order for every element in some set.
a partial order is a weaker variant of total order

Order
Duration
Interpretation

![](http://book.mixu.net/distsys/images/global-clock.png)

![](http://book.mixu.net/distsys/images/local-clock.png)

Vector clocks (time for causal order)
A Lamport clock

- Whenever a process does work, increment the counter
- Whenever a process sends a message, include the counter
- When a message is received, set the counter to max(local_counter, received_counter) + 1
