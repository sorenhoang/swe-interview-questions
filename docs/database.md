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

<details>

<summary>Explain write-ahead logging (WAL). </summary>

Write-Ahead Logging (WAL) is a database management technique used to ensure data integrity and durability in the event of a system crash or failure. In WAL, before any changes are made to the actual database, the intended changes are first recorded in a separate log file called the write-ahead log. This log contains a record of all modifications, including inserts, updates, and deletes. By writing the changes to the log before applying them to the database, WAL ensures that in the event of a crash, the database can be restored to a consistent state by replaying the log entries.

WAL provides several benefits, including improved performance, as it allows for batching of writes to the database, and enhanced recovery capabilities, as the log can be used to reconstruct the database state up to the point of failure. It is widely used in many relational database management systems, such as PostgreSQL and SQLite.

</details>

<details>
<summary>Explain and Compare OLTP vs OLAP </summary>

OLTP (Online Transaction Processing) and OLAP (Online Analytical Processing) are two different types of database systems designed for different purposes:

- **OLTP**: OLTP systems are designed to handle a large number of short, transactional operations, such as inserting, updating, and deleting records. They are optimized for fast query processing and maintaining data integrity in multi-user environments. OLTP databases are typically used in applications like e-commerce, banking, and customer relationship management (CRM) systems, where real-time data processing is essential.

- **OLAP**: OLAP systems, on the other hand, are designed for complex analytical queries and data analysis. They are optimized for read-heavy operations and support multidimensional data models, allowing users to perform complex calculations, aggregations, and data mining. OLAP databases are commonly used in business intelligence (BI) applications, data warehousing, and reporting systems, where large volumes of historical data need to be analyzed for decision-making purposes.

In summary, OLTP focuses on real-time transaction processing with high concurrency, while OLAP is geared towards complex data analysis and reporting with a focus on read performance.

</details>

<details>
<summary>What is eventual consistency? </summary>

Eventual consistency is a consistency model used in distributed systems and databases, where it is guaranteed that, given enough time, all replicas of a data item will converge to the same value. In an eventually consistent system, updates to a data item may not be immediately visible to all nodes or replicas, but over time, as changes propagate through the system, all replicas will eventually reflect the most recent update. This model is often used in NoSQL databases and distributed systems to achieve high availability and partition tolerance, allowing for temporary inconsistencies in favor of better performance and scalability.

</details>

<details>

<summary>What is a deadlock in databases? </summary>

A deadlock in databases occurs when two or more transactions are waiting for each other to release locks on resources, resulting in a situation where none of the transactions can proceed. For example, Transaction A holds a lock on Resource 1 and is waiting for a lock on Resource 2, while Transaction B holds a lock on Resource 2 and is waiting for a lock on Resource 1. Since neither transaction can acquire the locks they need, they are stuck in a deadlock.

Deadlocks can lead to performance issues and require the database management system (DBMS) to implement deadlock detection and resolution mechanisms. Common strategies for resolving deadlocks include aborting one of the transactions, rolling back its changes, and allowing the other transaction to proceed. To minimize the occurrence of deadlocks, developers can use techniques such as acquiring locks in a consistent order, using shorter transaction durations, and reducing lock contention.

</details>

<details>
<summary>What is read/write amplification?  </summary>

Read/write amplification refers to the phenomenon where the amount of data read from or written to storage is significantly larger than the actual amount of data being processed by an application. This can occur in various storage systems, including databases and file systems, and is often a result of underlying data structures, algorithms, or storage media characteristics.

Read amplification occurs when a read operation requires accessing more data than necessary, often due to the way data is organized or indexed. Write amplification happens when a write operation results in multiple writes to the storage medium, such as when updating data requires rewriting entire blocks or pages.

Both read and write amplification can lead to increased latency, reduced performance, and higher wear on storage devices, particularly in solid-state drives (SSDs). To mitigate read/write amplification, techniques such as data compression, efficient data structures, and optimized algorithms can be employed.

</details>

<details>

<summary>When should you denormalize data? </summary>

Denormalization is the process of intentionally introducing redundancy into a database by combining tables or adding redundant data to improve read performance. You should consider denormalizing data in the following scenarios:

1. **Performance Optimization**: When read operations are significantly more frequent than write operations, denormalization can reduce the number of joins required to retrieve data, leading to faster query performance.
2. **Complex Queries**: If your application frequently executes complex queries that involve multiple joins, denormalization can simplify these queries and improve their execution time.
3. **Reporting and Analytics**: In data warehousing or OLAP systems, denormalization can help optimize data retrieval for reporting and analytical purposes.
4. **Caching**: When you need to cache frequently accessed data, denormalization can help reduce the number of database calls required to fetch the data.
5. **Read-Heavy Workloads**: In scenarios where the workload is predominantly read-heavy, denormalization can help improve overall system performance.

However, it's important to weigh the benefits of denormalization against the potential drawbacks, such as increased storage requirements, data inconsistency risks, and more complex data maintenance. Denormalization should be approached carefully and typically after thorough analysis and testing.

</details>

<details>

<summary>What is SQL injection? How to avoid it? </summary>

SQL injection is a security vulnerability that occurs when an attacker is able to manipulate a SQL query by injecting malicious SQL code into input fields or parameters. This can lead to unauthorized access to the database, data leakage, data corruption, or even complete control over the database server.

To avoid SQL injection, consider the following best practices:

1. **Use Prepared Statements**: Utilize parameterized queries or prepared statements, which separate SQL code from data, preventing attackers from altering the query structure.
2. **Input Validation**: Validate and sanitize all user inputs to ensure they conform to expected formats and types.
3. **Least Privilege Principle**: Limit database user permissions to only what is necessary for the application to function, reducing the potential impact of an injection attack.
4. **Stored Procedures**: Use stored procedures for database operations, as they can help encapsulate SQL logic and reduce the risk of injection.
5. **Web Application Firewalls (WAFs)**: Implement WAFs to detect and block SQL injection attempts.

</details>

<details>
<summary>Can you reuse the compiled query multiple times? (does it help to speed up your application?) </summary>

Yes, you can reuse compiled queries multiple times, and doing so can help speed up your application. When a query is compiled, the database management system (DBMS) creates an execution plan that outlines how to retrieve the requested data. By reusing the compiled query, the DBMS can skip the compilation step for subsequent executions of the same query, which saves time and resources. This is particularly beneficial for applications that execute the same queries frequently, as it reduces the overhead associated with query parsing and optimization, leading to improved performance and faster response times.

</details>

<details>
<summary>How composite indexing works?</summary>

Composite indexing involves creating an index that includes multiple columns from a database table. This type of index is useful for optimizing queries that filter or sort data based on more than one column. When a composite index is created, the database management system (DBMS) organizes the index entries based on the combined values of the specified columns.

When a query is executed that uses the composite index, the DBMS can quickly locate the relevant rows by searching through the index using the values of the indexed columns. The order of the columns in the composite index is important, as it affects how efficiently the index can be used for different types of queries. For example, if a composite index is created on columns (A, B), it can efficiently support queries that filter on column A alone or on both columns A and B, but it may not be as effective for queries that filter only on column B.

</details>

<details>
<summary> How to write query to avoid full table scan? </summary>

To avoid a full table scan in your SQL queries, you can follow these best practices:

1. **Use Indexes**: Ensure that appropriate indexes are created on the columns used in the WHERE clause, JOIN conditions, and ORDER BY clauses.
2. **Selective Filtering**: Use highly selective conditions in the WHERE clause to reduce the number of rows scanned.
3. **Avoid Functions on Indexed Columns**: Refrain from using functions or calculations on indexed columns in the WHERE clause, as this can prevent the use of the index.
4. **Limit Result Set**: Use the LIMIT clause to restrict the number of rows returned by the query.
5. **Use EXISTS Instead of IN**: When checking for the existence of rows, use the EXISTS clause instead of IN, as it can be more efficient.
6. **Avoid Wildcards at the Beginning**: When using the LIKE operator, avoid starting the pattern with a wildcard (e.g., '%value'), as this can lead to a full table scan.
7. **Analyze Execution Plans**: Regularly review the query execution plans to identify and optimize queries that result in full table scans.

By following these practices, you can help ensure that your queries are optimized to use indexes effectively and avoid unnecessary full table scans.

</details>

<details>
<summary>Explain join algorithms in database engine </summary>

Database engines use various join algorithms to combine rows from two or more tables based on a related column. The most common join algorithms include:

1. **Nested Loop Join**: This algorithm iterates through each row of the outer table and, for each row, scans the entire inner table to find matching rows. It is simple but can be inefficient for large datasets.
2. **Merge Join**: This algorithm requires both input tables to be sorted on the join key. It iterates through both tables simultaneously, merging matching rows. Merge joins are efficient for large datasets when both tables are sorted.
3. **Hash Join**: This algorithm builds a hash table for the smaller of the two tables based on the join key. It then scans the larger table and probes the hash table to find matching rows. Hash joins are effective for large, unsorted datasets.

The choice of join algorithm depends on factors such as the size of the tables, the presence of indexes, and the distribution of data. Database engines use query optimizers to select the most appropriate join algorithm for a given query to ensure optimal performance.

</details>

<details>

<summary>How to rollback actually work? </summary>

Rollback is a database operation that reverses changes made during a transaction, restoring the database to its previous state before the transaction began. When a transaction is initiated, the database management system (DBMS) keeps track of all the changes made to the data. If an error occurs or if the transaction needs to be aborted for any reason, the rollback operation is triggered. During the rollback process, the DBMS uses a transaction log or undo log to identify the changes that were made and systematically reverses them. This ensures that any partial or incomplete changes do not persist in the database, maintaining data integrity and consistency.

</details>

<details>

<summary>How to avoid race condition in DB? Read/Write lock?</summary>

To avoid race conditions in a database, you can implement various concurrency control mechanisms, including:

1. **Locks**: Use read/write locks to control access to database resources. A read lock allows multiple transactions to read a resource simultaneously, while a write lock ensures exclusive access for a transaction that is modifying the resource. This prevents other transactions from reading or writing to the resource until the write lock is released.
2. **Transactions**: Use transactions to group multiple operations into a single unit of work. This ensures that either all operations are completed successfully, or none are applied, maintaining data integrity.
3. **Optimistic Concurrency Control**: Allow multiple transactions to proceed without locking resources, but check for conflicts before committing changes. If a conflict is detected, the transaction is rolled back and retried.
4. **Pessimistic Concurrency Control**: Lock resources as soon as they are accessed, preventing other transactions from accessing them until the lock is released.
5. **Isolation Levels**: Set appropriate isolation levels to control the visibility of changes made by concurrent transactions, reducing the likelihood of race conditions.

By implementing these strategies, you can effectively manage concurrent access to database resources and minimize the risk of race conditions.

</details>

<details>

<summary>What is Try-Confirm Cancel? </summary>

Try-Confirm-Cancel (TCC) is a distributed transaction management pattern used to ensure data consistency across multiple services or systems. It consists of three main phases:

1. **Try**: In this phase, the system attempts to reserve the necessary resources or perform preliminary operations required for the transaction. This may involve checking availability, locking resources, or preparing data without making permanent changes.
2. **Confirm**: If the Try phase is successful, the Confirm phase is executed, where the actual changes are committed to the database or system. This phase finalizes the transaction and makes the changes permanent.
3. **Cancel**: If the Try phase fails or if any issues arise during the Confirm phase, the Cancel phase is triggered. This phase rolls back any changes made during the Try phase, releasing any reserved resources and ensuring that the system remains in a consistent state.

TCC is commonly used in microservices architectures and distributed systems to manage complex transactions that span multiple services, ensuring data integrity and consistency even in the presence of failures.

</details>
