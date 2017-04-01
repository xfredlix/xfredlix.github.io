# SQL
- SQL is a programming language designed to manipulate and manage data stored in relational databases


### Relation Databases
- A relational database is a database that organizes information into one or more tables
- A table is a collection of data organized into rows and columns. Tables are sometimes referred to as relations
- A column is a set of data values of a particular type
- A row is a single record in a table
- All data stored in a relational database is of a certain data type. Some of the most common data types are:
  - Integer, a positive or negative whole number
  - Text, a text string
  - Date, the date formatted as YYYY-MM-DD for the year, month, and day
  - Real, a decimal value


### Manipulation
- A statement is text that the database recognizes as a valid command. Statements always end in a semi-colon ;
- CREATE TABLE is a clause. Clauses perform specific tasks in SQL. By convention, clauses are written in capital letters. Clauses can also be referred to as commands
- table_name refers to the name of the table that the command is applied to
- (column_1 data_type, column_2 data_type, column_3 data_type) is a parameter. A parameter is a list of columns, data types, or values that are passed to a clause as an argument. The order of columns determine which columns are first, second etc

CREATE statement creates a new table in the database
- CREATE TABLE table_name (
    column_1 data_type,
    column_2 data_type,
    column_3 data_type
  );

INSERT statement inserts new rows into a table
- INSERT INTO celebs (id, name, age) VALUES (1, 'Justin Bieber', 21);

SELECT statements are used to query/fetch data from a database. It always returns a new table called the result set. SELECT DISTINCT is used to return unique values in the result set. It filters out all duplicate values. The result set lists each column in the table exactly once
* is a special wildcard that allows you to select every column in a table without having to name each one individually
- SELECT name FROM celebs;

UPDATE statement edits a row in the table. celebs is the name of the table. SET is a clause that indicates the column to edit. WHERE is a clause that indicates which row(s) to update with the new column value
- UPDATE celebs SET age = 22 WHERE id = 1;

ALTER TABLE statement adds a new column to the table. celebs is the name of the table that is being changed. ADD COLUMN is a clause that lets you add a new column to a table. twitter_handle is the name of the new column being added. TEXT is the data type for the new column. NULL is a special value in SQL that represents missing or unknown data. Here, the rows that existed before the column was added have NULL values for twitter_handle
- ALTER TABLE celebs ADD COLUMN twitter_handle TEXT;

DELETE FROM statement deletes one or more rows from a table. WHERE is a clause that lets you select which rows you want to delete. Here we want to delete all of the rows where the twitter_handle column IS NULL. IS NULL is a condition in SQL that returns true when the value is NULL and false otherwise
- DELETE FROM celebs WHERE twitter_handle IS NULL;


### Queries

WHERE is a clause that indicates you want to filter the result set to include only rows where the following condition is true. Operators create a condition that can be evaluated as either true or false. Common operators used with the WHERE clause are:

= equals
!= not equals
> greater than
< less than
>= greater than or equal to
<= less than or equal to

LIKE is a special operator used with the WHERE clause to search for a specific pattern in a column. LIKE can be a useful operator when you want to compare similar values. Here, we are comparing two movies with the same name but are spelled differently. LIKE is not case sensitive. The _ means you can substitute any individual character here without breaking the pattern. The names Seven and Se7en both match this pattern
- SELECT * FROM movies WHERE name LIKE 'Se_en';

% is a wildcard character that matches zero or more missing letters in the pattern. A% matches all movies with names that begin with "A". %a matches all movies that end with "a"
- SELECT * FROM movies WHERE name LIKE '%man%';

The BETWEEN operator is used to filter the result set within a certain range. The values can be numbers, text or dates. This statement filters the result set to only include movies with names that begin with letters "A" up to but not including "J"
- SELECT * FROM movies WHERE name BETWEEN 'A' AND 'J';
In this statement, the BETWEEN operator is being used to filter the result set to only include movies with years between 1990 up to and including 2000
- SELECT * FROM movies WHERE year BETWEEN 1990 AND 2000;

AND is an operator that combines two conditions. Both conditions must be true for the row to be included in the result set
- SELECT * FROM movies WHERE year BETWEEN 1990 and 2000 AND genre = 'comedy';

The OR operator can also be used to combine more than one condition in a WHERE clause. The OR operator evaluates each condition separately and if any of the conditions are true then the row is added to the result set
- SELECT * FROM movies WHERE genre = 'comedy' OR year < 1980;

ORDER BY is a clause that indicates you want to sort the result set by a particular column either alphabetically or numerically
- SELECT * FROM movies ORDER BY imdb_rating DESC;

LIMIT is a clause that lets you specify the maximum number of rows the result set will have
- SELECT * FROM movies ORDER BY imdb_rating DESC LIMIT 3;


### Aggregate Functions

COUNT() is a function that takes the name of a column as an argument and counts the number of rows where the column is not NULL. Here, we want to count every row so we pass * as an argument
- SELECT COUNT(*) FROM fake_apps;

GROUP BY is a clause in SQL that is only used with aggregate functions. It is used in collaboration with the SELECT statement to arrange identical data into groups
- SELECT price, COUNT(*) FROM fake_apps GROUP BY price;

SUM() is a function that takes the name of a column as an argument and returns the sum of all the values in that column
- SELECT SUM(downloads) FROM fake_apps;

MAX() is a function that takes the name of a column as an argument and returns the largest value in that column
- SELECT MAX(downloads) FROM fake_apps;

MIN() is a function that takes the name of a column as an argument and returns the smallest value in that column
- SELECT MIN(downloads) FROM fake_apps;

The AVG() function works by taking a column name as an argument and returns the average value for that column
- SELECT AVG(downloads) FROM fake_apps;

ROUND() is a function that takes a column name and an integer as an argument. It rounds the values in the column to the number of decimal places specified by the integer
- SELECT price, ROUND(AVG(downloads), 2) FROM fake_apps GROUP BY price;


### Multiple Tables

- Imagine a database with two tables, artists and albums. An artist can produce many different albums, and an album is produced by an artist. One artist to many albums. The foreign key is put in the many albums table

- A primary key serves as a unique identifier for each row or record in a given table. The primary key is literally an id value for a record. By specifying that the id column is the PRIMARY KEY, SQL makes sure that:
  - None of the values in this column are NULL
  - Each value in this column is unique
  - A table can not have more than one PRIMARY KEY column
- CREATE TABLE artists (
    id INTEGER PRIMARY KEY,
    name TEXT
  );

- A foreign key is a column that contains the primary key of another table in the database. We use foreign keys and primary keys to connect rows in two different tables. One table's foreign key holds the value of another table's primary key. Unlike primary keys, foreign keys do not need to be unique and can be NULL

- A CROSS JOIN queries multiple tables by writing a SELECT statement with multiple table names separated by a comma. When querying more than one table, column names need to be specified by table_name.column_name
- SELECT albums.name, albums.year, artists.name FROM albums, artists;

- An INNER JOIN will combine rows from different tables if the join condition is true. - The most common type of join in SQL is an inner join
- SELECT * FROM albums JOIN artists ON albums.artist_id = artists.id;
  - SELECT * specifies the columns our result set will have. Here, we want to include every column in both tables
  - FROM albums specifies the first table we are querying
  - JOIN artists ON specifies the type of join we are going to use as well as the name of the second table. Here, we want to do an inner join and the second table we want to query is artists
  - albums.artist_id = artists.id is the join condition that describes how the two tables are related to each other. Here, SQL uses the foreign key column artist_id in the albums table to match it with exactly one row in the artists table with the same value in the id column. We know it will only match one row in the artists table because id is the PRIMARY KEY of artists

- A LEFT OUTER JOIN also combine rows from two or more tables, but unlike inner joins, they do not require the join condition to be met. Instead, every row in the left table is returned in the result set, and if the join condition is not met, then NULL values are used to fill in the columns from the right table
- The left table is simply the first table that appears in the statement. Here, the left table is albums. Likewise, the right table is the second table that appears. Here, artists is the right table
- SELECT * FROM albums LEFT JOIN artists ON albums.artist_id = artists.id;

- AS is a keyword in SQL that allows you to rename a column or table using an alias. The new name can be anything you want as long as you put it inside of single quotes. It is important to note that the columns have not been renamed in either table. The aliases only appear in the result set
- SELECT albums.name AS 'Album', albums.year, artists.name AS 'Artist' FROM albums JOIN artists ON albums.artist_id = artists.id WHERE albums.year > 1980;
