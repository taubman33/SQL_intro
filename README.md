[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)


## Joins

### Lecture Objectives: 
* Contrast relational and non-relational databases. ✅
* Create, set up, and seed a PostgreSQL database. ✅
* Execute SQL commands to perform CRUD actions. ✅
* Describe how to represent relationships in SQL databases. ✅
* Use JOIN to combine tables in a SELECT. 👈

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
