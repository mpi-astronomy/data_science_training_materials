### What is a database?

A database is a collection of data organized and stored in a computer system so it can be accessed and updated efficiently. 

There are a number of ways to organize the data and so there are a number of different ~types~ of databases. 

#### What is in a database?

#### Types of databases

Databases are sometimes referred to as Database Management Systems or DBMS, which is really the whole package of data and code
but I am using "databases" for short.

There are four main types of databases: relational, object-oriented, graph-based, and NoSQL. 

- A relational database (RDBMS) is a type of database that stores and provides access to data points that are related to one another.
  Relational databases are based on the relational model, an intuitive, straightforward way of representing data in tables.
  In a relational database, each row in the table is a record with a unique ID called the key. The columns of the table hold
  attributes of the data, and each record usually has a value for each attribute, making it easy to establish the relationships
  among data points. Most common in astronomy. Example: https://www.pragimtech.com/blog/contribute/article_images/2220211210231003/what-is-a-relational-database.jpg



Relational DBMSs are the most common and use a tabular structure to store data. 
Object-oriented DBMSs use an object-oriented model to store data, and Graph-based DBMSs use a graph structure to store data.
NoSQL DBMSs are a newer DBMS type that uses a non-tabular structure to store data.

Current market share by DBMS: https://en.wikipedia.org/wiki/Relational_database#Market_share as of January 2023.

And now: https://db-engines.com/en/ranking

#### Why use a database and not a FITS table or a big file?

- Dtabases can handle data that is larger than the RAM of your computer.
- Databases can handle querying tasks, including very complex queries, math, etc.
- Databases can handle indexing tasks and can be VERY fast.
- Databases can handle multiprocess/multithreaded access.
- Databases can handle access from network.
- Databases can watch for data integrity.
- Databases can update data easily
- Databases are reliable
- Databases can handle transactions and concurrent access
- Databases (+ ORMs) let you manipulate data in very programmer friendly way.

(List courtesy of Andrey https://stackoverflow.com/questions/2356851/database-vs-flat-files)
