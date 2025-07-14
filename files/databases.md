---
title: Using Databases Introduction
authors:
- name: Iva Momcheva
  affiliation: mpia
affiliations:
    - id: mpia
      institution: Max Planck Institute for Astronomy, Königstuhl 17, 69117 Heidelberg, Germany 
      ror: https://ror.org/01vhnrs90
      isni: 0000 0004 0491 677X
      department: Data Science Department
      address: Königstuhl 17
      city: Heidelberg
      country: Germany
      postal_code: 69117
date: 2023-12-08
---

## What is a database?

A database is a collection of data organized and stored in a computer system so it can be accessed and updated efficiently. 

There are a number of ways to organize the data and so there are a number of different ~types~ of databases. 

### What is in a database?

A database typically consists of the following components:

- Data: data is the actual information stored in the database. It can be further classified into user data, metadata, and application metadata.
- Hardware: Hardware includes every device that is useful for entering and saving data in the database, such as magnetic tapes and hard disks. 
- Software: Software serves the purpose of connecting the user with the database. Users can make modifications and accomplish other operations on the data using software. The software detemines the data access language.
- Users: Users are the most important component of a database as they are responsible for performing every function, big and small, on a database. From entering information into a database to saving and modifying this information, it is the user who is responsible for implementing different functions on the database. 

### Types of databases

Databases are sometimes referred to as Database Management Systems or DBMS, which is really the whole package of data and code
but I am using "databases" for short.

There are many different types of databases. Some examples inclide: relational, object-oriented, graph-based, key-value and NoSQL. In same cases you may also see object, graph, key-value, etc. databases being classified as NoSQL and NoSQL databases may have SQL-like interfaces. 

- A relational database (RDBMS) is a type of database that stores and provides access to data points that are related to one another.
  Relational databases are based on the relational model, an intuitive, straightforward way of representing data in tables.
  In a relational database, each row in the table is a record with a unique ID called the key. The columns of the table hold
  attributes of the data, and each record usually has a value for each attribute, making it easy to establish the relationships
  among data points. Most common in astronomy. Example: https://www.pragimtech.com/blog/contribute/article_images/2220211210231003/what-is-a-relational-database.jpg

- Object oriented databases are a computer data storage approach that manages data as "blobs" or "objects". Each object is typically associated with a variable amount of metadata, and a globally unique identifier. Examples: AWS S3, iTunes (?), https://res.cloudinary.com/practicaldev/image/fetch/s--xq9X76lU--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/yohz73d9ddpr8am0s7e4.jpg

- A graph database stores nodes and relationships instead of tables, or documents. Data is stored just like you might sketch ideas on a whiteboard. Your data is stored without restricting it to a pre-defined model, allowing a very flexible way of thinking about and using it. Facebook, Instagram, LinkedIn and Twitter all rely on graph databases and analytics to understand how users relate to each other and to connect users with the right content. Example: https://neo4j.com/developer/graph-database/

- NoSQL DBMSs are a newer DBMS type that uses a non-tabular structure to store data. When people use the term “NoSQL database”, they typically use it to refer to any non-relational database. Some say the term “NoSQL” stands for “non SQL” while others say it stands for “not only SQL”. Either way, most agree that NoSQL databases are databases that store data in a format other than relational tables. NoSQL databases emerged in the late 2000s as the cost of storage dramatically decreased and optimization to decrease data volume became less necessary.

- A key-value database (also known as a key-value store) is a type of noSQL database. A key-value database uses individual or combinations of keys to retrieve associated values. Together they are known as key-value pairs. These values can be anything from simple data types like strings or integers to complex objects with multiple nested values. Each key is a unique identifier that maps to a value or a location of data being stored. Example: https://d1.awsstatic.com/product-marketing/DynamoDB/PartitionKey.8dd0530a7f6d66d101f31de30db515564f4cf28a.png

Current market share by DBMS: https://en.wikipedia.org/wiki/Relational_database#Market_share as of January 2023.

And now: https://db-engines.com/en/ranking

### Why use a database and not a FITS table or a big file?

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

### Disadvantages

There are also some disadvantages to using database architecture:

- Setting up and maintaining a database can be complex, requiring specialized skills and resources.
- The purchase and maintenance of database software and hardware can be expensive.
- Large databases can be resource-intensive, and the performance of the system may suffer as the amount of data grows.
- A database may need to be redesigned or reconfigured as the amount of data grows or the number of users increases, which can be a time-consuming and complex process.

(List courtesy of Andrey https://stackoverflow.com/questions/2356851/database-vs-flat-files)


## Databases in Astronomy

There are lots of databases in astronomy. May of them have web interfaces. What are some databases that you use frequently?

Webpages are nice but reproducible they are not. In order to address this, may 

Astroquery: https://astroquery.readthedocs.io/en/latest/

Notes from BG workshop:
https://github.com/nden/astropy_bg_2023/blob/main/Archives/archive_exploration.ipynb

Go over archive, SDSS, HST and JWST. Finish with astrometry.net.

## SQL

Even if you live well, you have to at some point write a SQL query. 

SQL cheat sheet: https://learnsql.com/blog/sql-basics-cheat-sheet/sql-basics-cheat-sheet-a4.pdf

<img width="531" alt="Screen Shot 2023-12-08 at 12 25 58" src="https://github.com/mpi-astronomy/data_science_training_materials/assets/4562253/e0fa5b56-18f3-4517-8e69-ddc0e8e78ad8">

ADQL: 
![Screen Shot 2023-12-08 at 12 27 52](https://github.com/mpi-astronomy/data_science_training_materials/assets/4562253/0e33cf69-21c7-461a-a398-560e2c7c1d9c)

Foundations of astronomical data science:

https://datacarpentry.org/astronomy-python/

Full presentation: https://prezi.com/view/dCnsaMtMYwgf6NdMkGSX/
