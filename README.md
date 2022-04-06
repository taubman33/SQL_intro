[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)


# SQL JOINs

![](https://365datascience.com/resources/blog/2019-11-what-are-joins.jpg)

## Overview

In this lesson, we'll learn how to interact with and define associated data.
Utilizing the power of `joins`, we can join related data together utilizing `foreign key` references.

## Getting Started

- Fork and Clone

## Learning Objectives

- Create tables with foreign key references.
- Create join tables to represent many-to-many relationships.
- Insert rows in join tables to create many-to-many relationships.
- Select data about many-to-many relationships using join tables.

## Introduction

While it is conceivable to store all of the data that is needed for a particular domain model object or resource in a single table, there are numerous downsides to such an approach. For example, in sql, if we want to update the name `America` or `Ireland` to `United States of America` or `Republic Of Ireland`, we would have to update every single row in the table that referred to either of these places of origin. Thus, `redundancy` of common data points can make altering or updating these fields difficult.

Further, there are weak guarantees for the consistency and correctness of hard-coded fields in a single column; what prevents a developer who is working on a different feature from using `french` rather than `France` when inserting new rows into the a table? Leveraging table relations can improve `data integrity` and provide stronger guarantees regarding the consistency and correctness of what we store and retrieve from a database.

One of the key features of relational databases is that they can represent
relationships between rows in different tables.

Consider spotify, we could start out with two tables, `artist` and `track`.
Our goal now is to somehow indicate the relationship between an artist and a track.
In this case, that relationship indicates who performed the track.

You can imagine that we'd like to use this information in a number of ways, such as...

- Getting the artist information for a given track
- Getting all tracks performed by a given artist
- Searching for tracks based on attributes of the artist (e.g., all tracks
  performed by artists at Interscope)

## Setting Up Our Database

Let's build out a todo database, starting with todos and users.
Note how id's are PRIMARY KEYs, and relationships are established when these ids are referenced by other tables.

`seed.sql`

```sql
-- Your Code Here
CREATE TABLE authors(
    id VARCHAR(255) PRIMARY KEY,
    name VARCHAR(255),
    nationality VARCHAR(255)
);

CREATE TABLE books(
    id VARCHAR(255) PRIMARY KEY,
    title VARCHAR(255),
    description VARCHAR(255),
    completed BOOLEAN NOT NULL,
    author_id VARCHAR(255) REFERENCES authors(id)
);
-- Your Code Here
```

To `SELECT` information on two or more tables at ones, we can use a `JOIN`
clause. This will produce rows that contain information from both tables. When
joining two or more tables, we have to tell the database how to match up the
rows. (e.g. to make sure the author information is correct for each book).

This is done using the `ON` clause, which specifies which properties to match.

### Writing SQL JOINS

```sql
SELECT id FROM authors where name = 'J.K. Rowling';
SELECT * FROM books where author_id = 2;

SELECT * FROM books JOIN authors ON books.author_id = authors.id;
SELECT * FROM books JOIN authors ON books.author_id = authors.id WHERE authors.nationality = 'United States of America';
```

## You Do: Books and Authors 

See advanced_queries.sql in the
[library_sql](https://git.generalassemb.ly/sei-921/library_sql/blob/master/advanced_queries.sql)
exercise.

## Hungry for More? Less Common Joins

There are actually a number of ways to join multiple tables with `JOIN`, if
you're really curious, check out this article:

[A visual explanation of SQL Joins](http://blog.codinghorror.com/a-visual-explanation-of-sql-joins/)

## Bonus: Many-to-Many Relationships

We're not going to go in-depth with many-to-many relationships today, but lets
go over a simple example:

Consider if we wanted to add a categories model (e.g. fiction, non-fiction,
sci-fi, romance, etc). Books can belong to many categories (i.e. a book might be
a fiction/romance, or a history/non-fiction). And a given category might have
many books.

Because of this, we can't put a book_id column on categories, nor a category_id
column on books, either way, we might have more than one value in that field (a
no-no in terms of performance).

To solution is to create an additional table, which stores just the
relationships between the two tables. Such a table is called a join table, and
contains two foreign key columns.

In our example, we might create a table called 'categorizations', and it would
have a book_id and category_id. Each row would represent a specific book's
association with a specific category.

![many_to_many](images/many_to_many.png)

### Lecture Objectives - COMPLETE! 

* Contrast relational and non-relational databases. ✅
* Create, set up, and seed a PostgreSQL database. ✅
* Execute SQL commands to perform CRUD actions. ✅
* Describe how to represent relationships in SQL databases. ✅
* Use JOIN to combine tables in a SELECT. ✅

![celebrate](https://media.giphy.com/media/LSNqpYqGRqwrS/giphy.gif)

## Closing/Questions 

- What is the distinctive feature of a relational database?
- How is information stored in a relational database?
- What are the different types of relations that exist in a relational database?
- How do we indicate a one-to-many relationship in a database?


## Practice

The following resources are a great way to gain further familiarity with SQL. We
fully expect this to be a challenge.

- [Code School Try SQL](https://www.codeschool.com/courses/try-sql)
- [SQL for Beginners](https://www.codewars.com/collections/sql-for-beginners/):
  Created by WDI14 graduate.
- [The official PostgreSQL Documentation](https://www.postgresql.org/docs/9.3/static/index.html)
  is also very good, in particular:
  - [The preface](https://www.postgresql.org/docs/9.3/static/preface.html)
  - [The official tutorial](https://www.postgresql.org/docs/9.3/static/tutorial.html)
  - [The overview of SQL](https://www.postgresql.org/docs/9.3/static/sql.html)

## Additional Resources

- [Postgres Guide](http://postgresguide.com/)
- [SQL Zoo](https://sqlzoo.net/)
- [W3 Schools SQL tutorial](https://www.w3schools.com/sql/)
- [SQL Course](http://www.sqlcourse.com/)
- [Database Interview Questions](https://www.softwaretestinghelp.com/database-interview-questions/)

## [License](LICENSE)

1. All content is licensed under a CC­BY­NC­SA 4.0 license.
1. All software code is licensed under GNU GPLv3. For commercial use or
   alternative licensing, please contact legal@ga.co.
