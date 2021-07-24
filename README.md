# Introduction to Python 🐍 and SQL
Repository created in Datacamp curse of Introduction to Python and SQL.

# 📝 Class notes - Python:

<details>
<summary>Expandir</summary>

## Python Lists

<details>
<summary>Expandir</summary>

### Python Data Types:
- float: real numbers
- int: integer numbers
- str: string, text
- bool: True, False
  
```
height = 1.73
tall = True
```
=> Each variable represents single value

### Problems:

- Data Science: many data points are
- Height of entire family
  ```
  height1 = 1.73
  height2 = 1.68
  height3 = 1.71
  height4 = 1.89
  ```
=> It would be incovenient & counter-productive to create a new variable for each point collected

### Python List:

- ``` letters = [a, b, c] ```

A list is a way to give a single name to a collection of values of any type and with differents types.

### Subsetting Lists

<details>
<summary>Expandir</summary>

#### List slicing:

```
fam = ['liz', 1.73, 'emma', 1.68, 'mom', 1.71, 'dad', 1.89]
```
=> Allows to select multiple elements from a list, thus creating a new list. Is is possible by specifying a rangem, using a colon.

  [   start    :     end ]
    inclusive     exclusive
Ex.:
```
fam[3:5] = [1.68, 'mom]
```
</details>

### Manipulations Lists

<details>
<summary>Expandir</summary>

#### Delete list elements:

I could use the ```del``` statement to remove elements from my list. 
```
x = ["a", "b", "c", "d"]
del(x[1])
```
Pay attention here: as soon as you remove an element from a list, the indexes of the elements that come after the deleted element all change!

#### Behind the scenes (1):

What actually happens when I create a new list, x, like this?
```
x = ["a", "b", "c"]
```
In a simplified sense, I'm storing a list in your computer memory, and store the 'address' of that list, thereby where the list in my computer memory, in x.
This means that x doesn't actually contain all the list elements, it rather contains a reference to the list.
It's important say that for basic operations, the difference is not that important, but it becomes more so when I start copying lists.
Consider the situation when I want store the list x as a new variable y, by simply using the equals sign.
```
x = ["a", "b", "c"]
y = x
```
Let's now change the element with index one in the list y, like this.
```
['a', 'z', 'c']
```
If I check out x again, also the second element was changed. The explanetion for this is that when I copied x to y, with the equals sign, I copied the reference to the list, not the actual values themselves,
. Because both x and y point to this list, so the update is visible from both variables.

If I want to create a list y that points to a new list in the memory with the same values, I will need to use something else than the equals sign.
I could use the **list function** or use slicing to select all list elements explicitly, like this:
```
x = ["a", "b", "c"]
y = list(x)
y = x[:]
```
</details>
</details>

## Functions and Packages

<details>
<summary>Expandir</summary>

### Methods:

In Python, everything is an object, and each object has specific methods associated. Depending on the type of the object, list, string, float, whatever, the avaliable methods are different. 

### Packages:

Packages are like a directory of Python scripts where each scriptis a so-called module whose function is specify functions, methods and new Python types aimed at solving particular problems 

#### Selective import:

General imports, like ```import math```, make **all** functionality from the ```math``` package available to you. However, if you decide to only use a specific part of a package, you can always make your import more selective:
```
from math impor pi
```
</details>

## Numpy

<details>
<summary>Expandir</summary>

Numpy or Numeric Python is a Python package that, among others, provides a alternative to the regular python list: the Numpy array with this we can perform calculation solver entire arrays easily and fast.
It's possible because Numpy assumes that whole values are of a single type. Hence just make sure to pay attention when use arrays or list because they have different behavior.

### 2D Numpy Arrays:

Numpy was able to perform all calculations element-wise (i.e. element by element). For 2D numpy arrays this isn't any different! You can combine matrices with single numbers, with vectors, and with other matrices. Like this:
```
import numpy as np
np_mat = np.array([[1, 2],
                   [3, 4],
                   [5, 6]])
np_mat * 2
np_mat + np.array([10, 10])
np_mat + np_mat
```

<hr>

### Numpy: Basic Statitics

<details>
<summary>Expandir</summary>

#### Data analysis: 

A typical first step in analysing data, is getting to know my data in the first place. For the Numpy arrays before, this is pretty easy, because it isn't a lot of data. However, as a data scientist, you will be processing thousands, if not millions, or billions of numbers.

Let's consider that I am conducting a **City-wide survey** where I ask 5000 adults about their height and weight. I will end with a 2D numpy array, which I named np_city, that has 5000 rows, corresponding to 5000 people, and two columns, corresponding to the height and weight.

```
import numpy as np
np_city = ... # Implementation left out
np_city
```

<pre>
array([[1.64, 71.78],
       [1.37, 63.35],
       [1.6 , 55.09],
       ...,
       [2.04, 74.85],
       [2.04, 68.72],
       [2.01, 73.57]])
</pre>

It's a massive quantity of data for a person generate insights by yourself. However, I could generate summarizing statistics about my data.
Numpy assure speed to the analysis, because Numpy enforces a single data type in an array, it can drastically spped up the calculations.

#### Generate data:

It's possible simulated data with Numpy functions! I sampled two random distributions 5000 times to create the height and weight arrays, and then used column_stack to paste them together as two columns. Another awesome thing that Numpy can do! Another great tool to get some sense of your data is to visualize it.

Arguments for ```np.random.normal()```
- distribution mean
- distribution standart deviation
- number of samples

```
height = np.round(np.random.normal(1.75, 0.20, 5000), 2)
weight = np.round(np.random.normal(60.32, 15, 5000), 2)
np_city = np.column_stack((height, weight))

```

</details>

</details>

</details>

# 📝 Class notes - SQL:

<details>
<summary>Expandir</summary>

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
</details>