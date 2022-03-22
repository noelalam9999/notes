# Database
## What is a database
- A database is a piece of software specialized in efficiently storing and retrieving data in a persistent manner (i.e. to disk).
- Databases are mainly divided in 2 big families: relational and non-relational.
## Relational databases
- In a relational database you need to define in advance the structure of your data, and the relationship between data entities.
- The standard language for relational databases is SQL, which means “structured query language”. Popular SQL implementations are the MySQL, PostgreSQL, and SQLite databases.
- Data is divided into tables, and each table is divided into columns and rows, where each column can store a pre-defined data type.
- A unique identifier for a row in a table can be used as a “primary key”.
- When a table includes a reference to the primary key of another table it’s called a “foreign key”.
- Tables can have relations between them. The main type of relations are:
  - One to one
  - One to many
  - Many to many
- if one to one relationship (user and driving licence) it is still good to use different tables - modularization, as creation of one is not dependent on another.
- search by PK would be logarithmic as the keys can be sorted. If not on PK would be linear as would have to go through each row. that is why we use indexes.
- Indexes are sorted versions of the respective columns (with the associated primary key for each entry), which allow to improve query time from linear to logarithmic.
- indexes also have tradeoffs - read speed increases but write speed is slow as we have to rewrite in both table and the btree of the index. also storage but that is minor
- Joins are a way to combine data from different tables, by using a matching condition. Each operation involves two tables: a “left” and a “right” one, which can be joined in four ways:
  - Inner - Returns only records that satisfy the matching condition in both tables.
  - Full outer - Returns all records from both tables, matched where possible.
  - Left / right - Contains all records from one table, but only the ones that satisfy the matching condition from the other.

## Sharding and replicating
- Sharding means dividing database data into several partial instances, typically to store them on different machines, as it wouldn’t otherwise fit all in one place.
- Replicating means writing the same data in multiple places, for safety purposes.
- Both sharding and replicating present their challenges in terms of data atomicity and integrity guarantees, while maintaining high performance in reads and writes.

[SQL cheat sheet](https://learnsql.com/blog/sql-basics-cheat-sheet/sql-basics-cheat-sheet-a4.pdf)
[tutorial](https://sqlbolt.com/)