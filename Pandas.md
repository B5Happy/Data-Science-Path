# Pandas 

## Intro to Pandas 

### Importing the Pandas module

Pandas is a Python module for working with tabular data (i.e., data in a table with rows and columns). Tabular data has a lot of the same functionality as SQL or Excel, but Pandas adds the power of Python.

You get install it by *pip install pandas* and for more information, click [here](https://pandas.pydata.org/getpandas.html). 

The pandas module is usually imported at the top of a Python file under the alias pd.
```python
import pandas as pd
```

### Create a DataFrame

A DataFrame is an object that stores data as rows and columns. You can think of a DataFrame as a spreadsheet or as a SQL table. You can manually create a DataFrame or fill it with data from a CSV, an Excel spreadsheet, or a SQL query.

DataFrames have rows and columns. Each column has a name, which is a string. Each row has an index, which is an integer. DataFrames can contain many different data types: strings, ints, floats, tuples, etc.

You can pass in a dictionary to pd.DataFrame(). Each key is a column name and each value is a list of column values. The columns must all be the same length or you will get an error. Here’s an example:
```python
df1 = pd.DataFrame({
    'name': ['John Smith', 'Jane Doe', 'Joe Schmo'],
    'address': ['123 Main St.', '456 Maple Ave.', '789 Broadway'],
    'age': [34, 28, 51]
})
```
You can also add data using lists.

For example, you can pass in a list of lists, where each one represents a row of data. Use the keyword argument columns to pass a list of column names.
```python
df2 = pd.DataFrame([
    ['John Smith', '123 Main St.', 34],
    ['Jane Doe', '456 Maple Ave.', 28],
    ['Joe Schmo', '789 Broadway', 51]
    ],
    columns=['name', 'address', 'age'])
```
