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

### Comma Separated Variables (CSV)

We now know how to create our own DataFrame. However, most of the time, we'll be working with datasets that already exist. One of the most common formats for big datasets is the CSV.

The first row of a CSV contains column headings. All subsequent rows contain values. Each column heading and each variable is separated by a comma:
```python
column1,column2,column3
value1,value2,value3
```

When you have data in a CSV, you can load it into a DataFrame in Pandas using **.read_csv()**:
```python
pd.read_csv('my-csv-file.csv')
```

We can also save data to a CSV, using **.to_csv()**.
```python
df.to_csv('new-csv-file.csv')
```

If it's a larger DataFrame, it's helpful to be able to inspect a few items without having to look at the entire DataFrame.

The method **.head()** gives the first 5 rows of a DataFrame. If you want to see more rows, you can pass in the positional argument n. For example, **df.head(10)** would show the first 10 rows.

The method **df.info()** gives some statistics for each column.

### DataFrame Manipulation

If you want to take the average or plot a histogram of the ages. In order to do either of these tasks, you'd need to select only a column.

There are two possible syntaxes for selecting all values from a column:
- df.columnname
- df['columname']

To select two or more columns from a DataFrame, we use a list of the column names. To create the DataFrame shown above, we would use:
```python
df = sample[['columnone', 'columntwo']]
```

If we want to select a single row of data. we can do it by **sample.iloc[7]**. DataFrames are zero-indexed, meaning that we start with the 0th row and count up from there.
And to select multiple rows we can write **sample.iloc[2:7]** that select all rows from 2 to 6.

### Manipulation with Logic

You can use logic statement to retrive a set of data. For exmaple, if we want to select all row where price equal 10.
```python
df[df.price == 10]
```

We can use other logical statements, like:
- Greater than >
- Less than <
- Not Equal !=

You can expand your spesification with **|** means "or" and **&** means "and".

We could use the **isin** command to check that **df.name** is one of a list of values, for example:
```python
df[df.name.isin(['Antoine',
                'Sri',
                'Vignesh',
                'Koumar'])]
```

When we select a subset of a DataFrame using logic, we can end up with non-consecutive indices. This could be inelegant and makes it hard to use **.iloc()**.

We can fix this using the method **.reset_index()**.
