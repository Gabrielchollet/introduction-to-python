# Introduction to Python 🐍
Repository created in Datacamp curse of Introduction to Python.

# 📝 Class notes:

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

</details>
</details>