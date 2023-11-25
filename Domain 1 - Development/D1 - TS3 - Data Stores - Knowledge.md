# Relational and non-relational databases

# Create, read, update, and delete (CRUD) operations

# High-cardinality partition keys for balanced partition access

https://youtu.be/1xJTT4Jq7Hk - DynamoDB Partition Key: 5 Things You Must Know Before It's Too Late (AWS) - Abi Asija

High Cardinality = Large number of distinct values - even distribution over partitions, Hot partitions - rarely queried keys, always increasing values 

https://youtu.be/ErPrf74RUDY - All you need to know about DynamoDB Partitions - Alex DeBrie

10gb Partitions, single item actions(require full primary key), query, scan, Data model affects query effiecieny

# Cloud storage options (for example, file, object, databases)

# Database consistency models (for example, strongly consistent, eventually consistent)

https://youtu.be/WZqGS-wczaY - Data Consistency | Strong Consistency vs. Eventual Consistency | System Design for Beginners - Shiran Afergan

Strong consistency = lower performance vs Eventual , Different region or AZ, 

# Differences between query and scan operations

https://youtu.be/U-yApJ2_FCE - DynamoDB Scan vs Query - The Things You Need To Know - Be A Better Dev

Scan is very expensive - read capacity on every record in the table, pagination above 1mb, Query = Partition Key and Range Key - need the exact value, can query on GSIs

# Amazon DynamoDB keys and indexing

# Caching strategies (for example, write-through, read-through, lazy loading, TTL)

https://youtu.be/_JGgGR3Rp60 - How to make your DB fast by using Caching - Devlog #11 - SaaS Dev Log

Side Cache - App communicates seperately with cache and db , Read/Write-through Cache layer - every interaction with db happens with cache as well, Write-around - App talks to db and db talks to cache, write-behind = cache returns message that record is written but then writes to db

https://youtu.be/qa4dKkBiiCI - AWS Develeper Certification - Lazy Loading - Thornz Applications

Lazy loading = look in cache, hit = use, miss = fetch from DB, no stale data - TTL



General Caching

https://youtu.be/dGAgxozNWFE - Cache Systems Every Developer Should Know - ByteByteGo

# Amazon S3 tiers and lifecycle management

# Differences between ephemeral and persistent data storage patterns
