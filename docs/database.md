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

<details>
<summary>How does MVCC work?  </summary>

MVCC (Multi-Version Concurrency Control) works by maintaining multiple versions of data items to allow concurrent access without locking. When a transaction begins, it is assigned a unique timestamp. When a transaction reads data, it accesses the version of the data that was committed before its timestamp, ensuring a consistent view of the database.

When a transaction modifies data, instead of overwriting the existing data, MVCC creates a new version of the data item with a new timestamp. This allows other transactions to continue reading the old version while the new version is being created. Once the modifying transaction commits, the new version becomes visible to other transactions that start afterward.
This approach improves concurrency and performance by allowing readers and writers to operate simultaneously without blocking each other.

</details>

<details>

<summary>What is indexing and why it helps? </summary>

Indexing is a database optimization technique that involves creating data structures (indexes) to improve the speed of data retrieval operations. An index is similar to a book's index, which allows readers to quickly locate specific information without having to read through the entire book.

Indexes help by reducing the amount of data that needs to be scanned during query execution. Instead of searching through every row in a table, the database can use the index to quickly locate the relevant rows, significantly speeding up read operations. However, indexes can also introduce some overhead for write operations, as the index must be updated whenever data is inserted, updated, or deleted.

</details>

<details>
<summary>what are types of indexing </summary>

There are several types of indexing techniques used in databases to optimize data retrieval:

1. **B-Tree Indexing**: A balanced tree structure that maintains sorted data and allows for efficient insertion, deletion, and search operations. It is widely used in relational databases.
2. **Hash Indexing**: Uses a hash function to map keys to specific locations in a hash table. It provides fast lookups for equality comparisons but is not suitable for range queries.
3. **Bitmap Indexing**: Uses bit arrays (bitmaps) to represent the presence or absence of values in a column. It is efficient for columns with low cardinality (few unique values).
4. **Full-Text Indexing**: Designed for searching large text fields, it allows for efficient searching of words and phrases within text data.
5. **Spatial Indexing**: Used for geographic data, it allows for efficient querying of spatial relationships, such as proximity and containment.
6. **Clustered Indexing**: Determines the physical order of data in a table based on the indexed column(s). A table can have only one clustered index.
7. **Non-Clustered Indexing**: Creates a separate structure from the data table, allowing for multiple non-clustered indexes on a single table.
8. **Composite Indexing**: An index that includes multiple columns, allowing for efficient querying based on combinations of those columns.
9. **Unique Indexing**: Ensures that the indexed column(s) contain unique values, preventing duplicate entries in the database.

</details>

<details>
<summary>WWhat is query execution plan? </summary>

A query execution plan is a detailed roadmap that a database management system (DBMS) creates to execute a SQL query efficiently. It outlines the steps and methods the DBMS will use to retrieve the requested data, including the order of operations, the use of indexes, join methods, and data access paths.
The execution plan helps optimize query performance by allowing the DBMS to choose the most efficient way to execute the query based on factors such as data distribution, available indexes, and system resources. Database administrators and developers can analyze execution plans to identify performance bottlenecks and optimize queries for better efficiency.

</details>

<details>
<summary>Explain Database statistics </summary>

Database statistics are metadata that provide information about the distribution and characteristics of data within database tables and indexes. These statistics include details:

- Number of rows in a table
- Distribution of values in columns
- Number of distinct values
- Data density
- Index usage patterns
- Histograms for data distribution
- Average row size
- Null value counts
- Page and extent information

Database management systems (DBMS) use these statistics to optimize query execution plans. By analyzing the statistics, the DBMS can make informed decisions about the most efficient way to execute a query, such as which indexes to use, the join order of tables, and the methods for data retrieval. Keeping database statistics up-to-date is crucial for maintaining optimal query performance, as outdated statistics can lead to suboptimal execution plans and slower query response times.

</details>

<details>
<summary>What is sharding in databases? </summary>

Sharding is a database architecture technique that involves partitioning a large database into smaller, more manageable pieces called shards. Each shard is a separate database instance that contains a subset of the overall data. Sharding is used to improve performance, scalability, and availability of databases by distributing the data across multiple servers or nodes.

Sharding can be done based on various criteria, such as range-based sharding (dividing data based on a specific range of values), hash-based sharding (using a hash function to determine the shard for each data item), or geographic sharding (distributing data based on geographic location). By spreading the data across multiple shards, the database can handle larger volumes of data and higher levels of traffic, while also reducing the load on individual servers.
</details>

<details>
<summary>Eplain Sharding vs partitioning</summary>

Sharding and partitioning are both techniques used to divide a database into smaller, more manageable pieces, but they differ in their scope and implementation:

- **Sharding**: Involves distributing data across multiple database instances or servers, with each shard being a separate database that contains a subset of the overall data. Sharding is typically used for horizontal scaling, allowing the database to handle larger volumes of data and higher traffic by spreading the load across multiple machines. Each shard operates independently, and queries may need to be routed to the appropriate shard based on the sharding key.
- **Partitioning**: Refers to dividing a single database table into smaller, more manageable segments called partitions. Partitioning is usually done within a single database instance and is used to improve query performance and manageability. Partitions can be created based on various criteria, such as range, list, or hash partitioning. Queries can be optimized to access only the relevant partitions, reducing the amount of data that needs to be scanned.

In summary, sharding involves distributing data across multiple database instances for scalability, while partitioning involves dividing a single table within a database for performance optimization.
</details>
