Gotchas
1. Exclusive queues do not survive cluster failovers - they cannot be highly available
2. Requeued messages are put on the *front* of the queue, not the back
3. The mandatory flag for producers ensures a message reaches *at least* one queue. Be wary of wildcard queues that may catch every message.
