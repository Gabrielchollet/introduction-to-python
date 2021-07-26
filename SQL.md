# 📝 Class notes - SQL:

## Selecting columns

<details>
<summary>Expandir</summary>

SQL, which stands for _Structured Query Language_, is a language for interacting with data stored in something called a relational database.
You can think of a relational database as a collection of tables. A table is just a set of rows and columns, like a spreadsheet, which represents exactly one type of entity. For example, a table might represent employees in a company or purchases made, but not both.
Each row, or _record_, of a table contains information about a single entity. For example, in a table representing employees, each row represents a single person. Each column, or _field_, of a table contains a single attribute for all rows in the table. For example, in a table representing employees, we might have a column containing first and last names for all employees.

### SELECTing single columns

A _query_ is a request for data from a database table (or combination of tables). Querying is an essential skill for a data scientist, since the data you need for your analyses will often live in databases.
The table of employees might look something like this:
<pre>
| id 	| name    	| age 	| nationality 	|
|----	|---------	|-----	|-------------	|
| 1  	| Jessica 	| 22  	| Ireland     	|
| 2  	| Gabriel 	| 48  	| France      	|
| 3  	| Laura   	| 36  	| USA         	|
</pre>

In SQL, you can select data from a table using a ```SELECT``` statement. For example, the following query selects the ```name``` column from the ```people``` table:
```
SELECT name 
FROM people;
```
In this query, ```SELECT``` and ```FROM``` are called keywords. In SQL, keywords are not case-sensitive, which means you can write the same query as:
```
select name 
from people;
```
That said, it's good practice to make SQL keywords uppercase to distinguish them from other parts of your query, like column and table names.
It's also good practice to include a semicolon at the end of your query. This tells SQL where the end of your query is!
<hr>

### SELECTing multiple columns:

To select multiple columns from a table, simply separate the column names with commas!
For example, this query selects two columns, ```name``` and ```birthdate```, from the ```people``` table:
```
SELECT name, birthdate
FROM people;
```

Sometimes, you may want to select all columns from a table. Typing out every column name would be a pain, so there's a handy shortcut:
```
SELECT *
FROM people;
```

If you only want to return a certain number of results, you can use the LIMIT keyword to limit the number of rows returned:
```
SELECT *
FROM people
LIMIT 10;
```
<hr>

### SELECT DISTINCT

Often your results will include many duplicate values. If you want to select all the unique values from a column, you can use the ```DISTINCT``` keyword.

This might be useful if, for example, you're interested in knowing which languages are represented in the ```films``` table:
```
SELECT DISTINCT language
FROM films;
```
Remember, you can check out the data in the tables by clicking on the table name!

<hr>

### Learning to COUNT

What if you want to count the number of employees in your employees table? The ```COUNT()``` function lets you do this by returning the number of rows in one or more columns.

For example, this code gives the number of rows in the people table:
```
SELECT COUNT(*)
FROM people;
```

As you've seen, ```COUNT(*)``` tells you how many rows are in a table. However, if you want to count the number of non-missing values in a particular column, you can call ```COUNT()``` on just that column.
For example, to count the number of birth dates present in the ```people``` table:
```
SELECT COUNT(birthdate)
FROM people;
```
It's also common to combine ```COUNT()``` with ```DISTINCT``` to count the number of _distinct_ values in a column.

For example, this query counts the number of distinct birth dates contained in the ```people``` table:
```
SELECT COUNT(DISTINCT birthdate)
FROM people;
```

</details>

## Filtering rows


<details>
<summary>Expandir</summary>

### WHERE IN:

As you've seen, ```WHERE``` is very useful for filtering results. However, if you want to filter based on many conditions, ```WHERE``` can get unwieldy. For example:
```
SELECT name
FROM kids
WHERE age = 2
OR age = 4
OR age = 6
OR age = 8
OR age = 10;
```
Enter the ```IN``` operator! The ```IN``` operator allows you to specify multiple values in a ```WHERE``` clause, making it easier and quicker to specify multiple ```OR``` conditions! Neat, right?
So, the above example would become simply:
```
SELECT name
FROM kids
WHERE age IN (2, 4, 6, 8, 10);
```
<hr>

### Introduction to NULL and IS NULL:

In SQL, ```NULL``` represents a missing or unknown value. You can check for ```NULL``` values using the expression ```IS NULL```. For example, to count the number of missing birth dates in the ```people``` table:
```
SELECT COUNT(*) 
FROM people
WHERE birthdate IS NULL;
```
As you can see, ```IS NULL``` us useful when combined with ```WHERE``` to figure out what data you are missing.
Sometimes, you will want to filter out missing values so you only get results which are not `NULL`. To do thism you can use the `IS NOT NULL` operator.
For example, this query gives the names of all people whose birth dates are _not_ missing in the `people` table.
```
SELECT name 
FROM people
WHERE birthdate IS NOT NULL;
``` 

<hr>

### LIKE and NOT LIKE:

As you are seen, the `WHERE` clause can be used to filter text data. However, so far you've been able to filter by specifying the exact text you're interested in. In the real world, often you will want to search for a _pattern_ rather than a specific text string. 
In SQL, the `LIKE` operator can be used in a `WHERE` clause to search for a pattern in a column. To accomplish this, you use something called a _wildcard_ as a placeholder for some other values. There are two wildcards you can use with `LIKE`:
The `%` wildcard will match zero, one, or many characters in text. For example, the following query matches companies like 'Data', 'DataC', 'DataCamp', 'DataMind', and so on:
```
SELECT name 
FROM companies
WHERE name LIKE 'Data%';
```
> This wildcard has a same behavior of the wildcard character of Linux terminal * that could be understand like "anything".

The `_` wildcard will match a _single_ character. For example, the following query matches companies like 'DataCamp', 'DataComp', and so on:
```
SELECT names
FROM companies
WHERE name LIKE 'DataC_mp';
```
You can also use `NOT LIKE` operator to find records that _don't_ match the pattern you specify.

</details>

## Aggregate Functions

<details>
<summary>Expandir</summary>

Often, you will want to perform some calculation on data on the database. SQL provides a few functions, called _aggregate functions_, to help you out with this.
For example,
```
SELECT AVG(budget)
FROM films;
``` 
The `SUM()` function returns the result of adding up the numeric values in a column:
```
SELECT SUM(budget)
FROM films;
```
You can probably guess what the `MIN()` function does!

<hr>

### It's AS simple AS aliasing
You may have noticed in the first exercise of this chapter that the column name of your result was just the name of the function you used. For example,
```
SELECT MAX(budget)
FROM films;
```
gives you a result with one column, named `max`. But what if you use two functions like this?
```
SELECT MAX(budget), MAX(duration)
FROM films;
```
Well, then you'd have two columns named `max`, which isn't very useful!

To avoid situations like this, SQL allows you to do something called _aliasing_. Aliasing simply means you assign a temporary name to something. To alias, you use the `AS` keyword, which you've already seen earlier in this course.

For example, in the above example we could use aliases to make the result clearer:
```
SELECT MAX(budget) AS max_budget,
       MAX(duration) AS max_duration
FROM films;
```
Aliases are helpful for making results more readable!

</details>

## Sorting and grouping

<details>
<summary>Expandir</summary>

### ORDER BY:

IN SQL, the `ORDER BY` keyword is used to sort results is ascending or descending order according to the values of one or more columns.
By default `ORDER BY` will sort in ascending order. If you want to sort the results in descending order, you can use the `DESC` keyword. For example,
```
SELECT title
FROM films
ORDER BY release_year DESC;
```
<hr>

### Sorting multiple columns:

`ORDER BY` can also be used to sort on multiple columns. It will sort by the first column
</details>