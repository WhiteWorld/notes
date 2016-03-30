# DB

### 论文

[Megastore: Providing Scalable, Highly Available Storage for Interactive Services](http://research.google.com/pubs/pub36971.html)
[Spanner: Google's Globally-Distributed Database](http://research.google.com/archive/spanner.html)
[Large-scale Incremental Processing Using Distributed Transactions and Notifications](http://research.google.com/pubs/pub36726.html)
[F1 - The Fault-Tolerant Distributed RDBMS Supporting Google's Ad Business](http://research.google.com/pubs/pub38125.html)


### 临时资料
Google Percolator
http://blog.octo.com/en/my-reading-of-percolator-architecture-a-google-search-engine-component/
http://www.slideshare.net/mikejf12/an-introduction-to-google-percolator

### LevelDB

LevelDB is a fast key-value storage library written at Google that provides an ordered mapping from string keys to string values.

Features

- Keys and values are arbitrary byte arrays.
- Data is stored sorted by key.
- Callers can provide a custom comparison function to override the sort order.
- The basic operations are Put(key,value), Get(key), Delete(key).
- Multiple changes can be made in one atomic batch.
- Users can create a transient snapshot to get a consistent view of data.
- Forward and backward iteration is supported over the data.
- Data is automatically compressed using the Snappy compression library.
- External activity (file system operations etc.) is relayed through a virtual interface so users can customize the operating system interactions.

Limitations

- This is not a SQL database. It does not have a relational data model, it does not support SQL queries, and it has no support for indexes.
- Only a single process (possibly multi-threaded) can access a particular database at a time.
- There is no client-server support builtin to the library. An application that needs such support will have to wrap their own server around the library.


### CockroachDB

### TiDB

### RocksDB
