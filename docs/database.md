<!-- markdownlint-disable MD033 -->
# Database Questions

<details>
<summary>What are ACID properties? </summary>

ACID stands for Atomicity, Consistency, Isolation, and Durability. These properties ensure reliable processing of database transactions:

- **Atomicity**: Ensures that a transaction is treated as a single unit, which either completes entirely or not at all.
- **Consistency**: Ensures that a transaction brings the database from one valid state to another, maintaining database invariants.
- **Isolation**: Ensures that concurrent transactions do not interfere with each other, maintaining data integrity.
- **Durability**: Ensures that once a transaction is committed, it remains so, even in the event of a system failure.

</details>

<details>

<summary>What are BASE properties? </summary>

BASE stands for Basically Available, Soft state, Eventual consistency. These properties are often associated with NoSQL databases:

- **Basically Available**: The system guarantees availability, meaning that it will respond to requests, but not necessarily with the most recent data.
- **Soft state**: The state of the system may change over time, even without input, due to eventual consistency.
- **Eventual consistency**: The system will eventually become consistent over time, meaning that all replicas will converge to the same value if no new updates are made.
  
</details>

<details>
<summary>Explain transactions.  </summary>

A transaction is a sequence of one or more database operations that are treated as a single unit of work. Transactions are used to ensure data integrity and consistency, especially in multi-user environments. They follow the ACID properties to guarantee that either all operations within the transaction are completed successfully, or none are applied, maintaining the database's state.

</details>

<details>
<summary>What are isolation levels?  </summary>

Isolation levels define the degree to which the operations in one transaction are isolated from those in other concurrent transactions. Common isolation levels include:

- **Read Uncommitted**: Allows transactions to read data that has not yet been committed, leading to potential dirty reads.
- **Read Committed**: Ensures that a transaction can only read data that has been committed, preventing dirty reads.
- **Repeatable Read**: Guarantees that if a transaction reads a row, it will see the same data if it reads that row again, preventing non-repeatable reads.
- **Serializable**: The highest isolation level, ensuring complete isolation from other transactions, effectively serializing concurrent transactions.

Each level balances performance and data integrity differently, with higher isolation levels typically resulting in reduced concurrency and increased locking.
</details>

<details>
<summary>What is MVCC and how it works?  </summary>

MVCC stands for Multi-Version Concurrency Control. It is a database management technique used to handle concurrent transactions without locking the database rows. MVCC allows multiple versions of a data item to exist simultaneously, enabling readers to access a snapshot of the data without being blocked by writers.

When a transaction modifies data, instead of overwriting the existing data, MVCC creates a new version of the data item. Each transaction sees a consistent snapshot of the database as it was at the start of the transaction. This means that readers can continue to access the old version of the data while writers create new versions, thus improving concurrency and performance.
</details>

<details>
<summary>What are Serializable and how does it work?  </summary>

Serializable is the highest isolation level in database management systems. It ensures that transactions are executed in such a way that the end result is the same as if the transactions were executed serially, one after the other, without any overlap. This isolation level prevents phenomena such as dirty reads, non-repeatable reads, and phantom reads by ensuring that transactions do not interfere with each other.

To achieve serializability, the database system may use techniques such as locking, timestamp ordering, or optimistic concurrency control. These methods ensure that transactions are executed in a manner that maintains data integrity and consistency, even in a highly concurrent environment.
</details>

<details>

<summary>Dirty read vs non-repeatable read vs phantom read. </summary>

- **Dirty Read**: Occurs when a transaction reads data that has been modified by another transaction but not yet committed. If the other transaction is rolled back, the data read becomes invalid.
- **Non-Repeatable Read**: Happens when a transaction reads the same row twice and gets different data each time because another transaction has modified and committed changes to that row in between the two reads.
- **Phantom Read**: Occurs when a transaction re-executes a query and finds that new rows have been added or existing rows have been deleted by another committed transaction since the initial read, leading to different results.

**Isolation levels to prevent them:**

- Dirty Read: Prevented by Read Committed isolation level.
- Non-Repeatable Read: Prevented by Repeatable Read isolation level.
- Phantom Read: Prevented by Serializable isolation level.

</details>
