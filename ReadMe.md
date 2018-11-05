# Intro to NumPy

## What's NumPy ?

NumPy is a  powerful Python module, which stands for Numerical Python. Numpy is the fundamental package for scientific computing.

NumPy has many feature including large, multi-dimensional arrays and matrices, along with a large collection of high-level mathematical functions to operate on these arrays.

## Let's start coding !!

### Importing NumPy

To use NumPy we have to import it.

```python
import numpy as np 
```

Writing as np allows us to use np as a shorthand for NumPy, which saves us time.


### NumPy Arrays

The array holds and represents any regular data in a structured way.
Arrays are powerful because it give us special ways of performing mathematical operations.

```python
my_array = np.array([1, 2, 3, 4, 5, 6])
```

We can transform a regular list into a NumPy array

```python
my_list = [1, 2, 3, 4, 5, 6]
np_array = np.array(my_list)
```

#### Two-Dimensional Arrays

We can create an array of arrays and it's named a two-dimensional array.

```python
sample = np.array([1, 2, 3, 4, 5], [6, 7, 8, 9, 10], [11, 12, 13, 14,15])
```
A two-dimensional array is a list of lists where each list has the same number of elements. Here are some examples that are not two-dimensional arrays.
```python
np.array([[29, 49,  6], 
          [77,  1]])
```
This code will not run because the [] for the outer lists are missing:
```python
np.array([68, 16, 73],
         [61, 79, 30])
```

### Creating an Array from a CSV 

Typically, you won't be entering data directly into an array. Instead, you'll be importing the data from somewhere else.

We're able to transform CSV (comma-separated values) files into arrays using the np.genfromtxt() function:

Create a test.csv in excel(when you save your file save it as .csv)

```python
csv_array = np.genfromtxt('test.csv', delimiter=',')

print(csv_array)
```

> In this case, our file sample.csv has values separated by commas, so we use delimiter=',', but sometimes you could find files with other delimiters.

> Print to see array.

### Operations with NumPy Arrays 

Generally, NumPy arrays are more efficient than lists.

Let's see it, by comparing how to add a number to each value in a python list versus a NumPy array: 

```python
# With a list
l = [1, 2, 3, 4, 5]
l_plus_3 = []
for i in range(len(l)):
    l_plus_6.append(l[i] + 6)
```

```python
# With an array
a = np.array(l)
a_plus_6 = a + 6
```

Squaring each value:
```python
# With an array
a ** 2
```

When adding or subtracting arrays in NumPy, each element will be added/subtracted to its matching element :
```python
a = np.array([1, 2, 3, 4, 5])
b = np.array([6, 7, 8, 9, 10])
c = a + b
print(c)
[ 7,  9, 11, 13, 15]
```


> To find more check [this docs](https://www.scipy-lectures.org/intro/numpy/operations.html)

