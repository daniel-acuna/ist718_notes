# Basic Python
Lecturer: Prof. Daniel Acuña  
Scriber: Lizhen Liang & Yimin Xiao  

## Jupyter notebook
**Jupyter notebook** is the main tool to use in IST718

Modes:
1. **Command mode**
    - Press 'Esc' to enter command mode when from edit mode
    - The edge of the cell will turn blue in command mode
    - Press 'A' to add cell above or 'B' to add cell below, press 'D' twice to delete a cell 
    - Press 'M' to make the cell a markdown cell, press 'Y' to make the cell a ipython cell
    - Press 'Enter' to enter edit mode from command mode
2. **Edit mode**
    - Press enter to enter edit mode in commend mode
    - The edge of the cell will turn green in edit mode

## Python Basic

There are important differences between Python and other programming language:
- Python is a kind of dynamically typed language, which means we don't need to state the type of variables before creating them.
- Python code blocks are seperated by indentions / spaces rather then brackets.

There're four basic data type in Python:
- **tuple**: immutable collection (if we want to define a tuple with only one element, we define it like:```(16, )``` 
- **list**: all-purpose container for any data types
- **set**: a container for unordered, unique values
- **dict**: for storing maps of values (key/value pairs)

**Python strings are very similar to a list**: you can access the element in a string just like in a list.
**Lambda**: Anonymous function, a function with no name and we don't need to actually define a function when using lambda.

### Example
1. How to reverse a list?
```Python
A = [1,2,3,4,5,6]
B = []
for i in range(len(A)):
    B.append(A[len(A) - 1 - i])
```
2. Determine whether a number is a prime number?
```Python
def is_prime(n):
    for i in range(2, n):
        if n % i == 0:
            return False
        else:
            return True
```
### Comprehensions
A list comprehension consists of the following parts:
  - An **Input Sequence**.
  - A **Variable** representing members of the input sequence.
  - An **Optional Predicate Expression**.
  - An **Output Expression** producing elements of the output list from members of the Input Sequence that satisfy the predicate.

## Numpy, Pandas and Matplotlib and other packages

### Numpy
```Python
import numpy as np
```
- Deal with algebra calculation
- More efficient due to the compact implementation of vector, matrix, etc

**Numpy arrays**: only stores elements of the same data type. Elements in a array can be accessed, selected and modified like list.
**Random number generation**: 
```Python
 np.random.random(size = (5, 5))
 ```
Normal distributed ramdom numbers:
```Python
np.random.normal()
```
**Aggregate operations**: 
```Python
a.mean(axis = 0)
a.transpose()
a.sum()
```
**Broadcast**: operation to all elements in the array.

**Normalization / regularization**: mapping all the elements to between 0 and 1

**Convoluted way to compute the pi**

Given a circle with radius R = 1:
Throw dot into a one by one square that includes the given circle.
To check if a dot is in the circle or not: if the distance from the dot to point (0,0) is greater than 1, them the dot is outside the circle. The proportion between the dots inside the circle and the area of the inside the square equals to pi / 4. With more dots, we can get a more accurate calcutation of pi.


### Pandas
```Python
import pandas as pd
```
**Store "spreadsheet" with names for columns and different datatype**
The creator of Pandas created Pandas mostly in order to implement time series functions, so time series is the part where Pandas really shines.

Basic data structure
- `Series(labeled list, column)`
- `DataFrame(table)`

Types: `pd.DataFrame()`, `pd.Timestamp()`, `pd.Series()`, `pd.Categorical()`, etc.   

Locate an element: `df.loc(row name, column name)` or `df.iloc(row index, column index)`

Axis:
- Axis = 0: do by column; 
- Axis = 1: do by row;
- Default = 0

`Df.apply()`: apply a function (arbitrary) to the whole column  
**Applymap**: apply to all the cells  
**Plotting**: `pd.plot(x=‘’, y=‘’, kind=’scatter')`  

### Scipy
**Scientific functionalities**, such as statistics
