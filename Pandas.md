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

### DataFrame Selection

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

### Selection with Logic

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

## Manipulation of Dataframes

### Intro 

We will learn of to modify a Dataframe like:
-Adding columns
-How to use lambda function
-Renaming columns

### How to add a column

We might want to add a new information.
So we can add a new column, by giving a list of the same length as the existing DataFrame.
For example:
```python
df['columnName'] = ['same', 'length', 'data']
```

If All the new rows has the same value. We can add like this:
```python
df['Super'] = True
```

Finally, you can add a new column by performing a function on the existing columns.
```python
df['After Tax'] = df.Price * 0.20
```

More over we can use **apply** function to apply a function to evry value in a particular column.
For example, if we want to uppercase all first name:
```python
from string import upper

df['First_name'] = df.FirstName.apply(upper)
```

### Lambda Function

A lambda function is a way of defining a function in a single line of code. Usually, we would assign them to a variable.

For example, the following lambda function multiplies a number by 2 and then adds 3:
```python
mylambda = lambda x: (x * 2) + 3
print(mylambda(5))
# Output
13
```

We can make our lambdas more complex by using a modified form of an if statement.

Suppose we want success if the statement is true else fail.
```python
# For a normal Function
def myfunction(x):
    if x == true:
        return 'Success'
    else:
        return 'Fail'

# For lambda Function
myfunction = lambda x: 'Success' if 'Success' == True else 'Fail'

# syntax
lambda x: [OUTCOME IF TRUE] \
    if [CONDITIONAL] \
    else [OUTCOME IF FALSE]

```

In Pandas, we can use lambda functions to perform complex operations on columns. For example, suppose that we want to create a column containing the email provider for each email address in the following table:
```python
df['Email Provider'] = df.Email.apply(
    lambda x: x.split('@')[-1]
    )
```

We can also operate on multiple columns at once. If we use apply without specifying a single column and add the argument axis=1, the input to our lambda function will be an entire row, not a column. To access particular values of the row, we use the syntax row.column_name or row[‘column_name’].

Suppose we have a table representing a grocery list:

| Item	       | Price	| Is taxed?  |
| ------------ | :----: | ----------:|
| Apple	       | 1.00	| No         |
| Milk	       | 4.20	| No         |
| Paper Towels | 5.00	| Yes        |
| Light Bulbs  | 3.75	| Yes        |

If we want to add in the price with tax for each line, we’ll need to look at two columns: Price and Is taxed?.

If Is taxed? is Yes, then we’ll want to multiply Price by 1.075 (for 7.5% sales tax).

If Is taxed? is No, we’ll just have Price without multiplying it.

We can create this column using a lambda function and the keyword axis=1:
```python
df['Price with Tax'] = df.apply(lambda row:
     row['Price'] * 1.075
     if row['Is taxed?'] == 'Yes'
     else row['Price'],
     axis=1
)
```

### Renaming a Columns

When we get our data from other sources, we often want to change the column names.
You can change all of the column names at once by setting the .columns property to a different list. 
```python
df = pd.DataFrame({
    'name': ['John', 'Jane', 'Sue', 'Fred'],
    'age': [23, 29, 21, 18]
})
df.columns = ['First Name', 'Age']
```
>This command edits the existing DataFrame df.


Or we can rename individual columns by using the .rename, for example:
```python
df = pd.DataFrame({
    'name': ['John', 'Jane', 'Sue', 'Fred'],
    'age': [23, 29, 21, 18]
})
df.rename(columns={
    'name': 'First Name',
    'age': 'Age'},
    inplace=True)
```

## Pandas Aggregates

Aggregate is using one or more operations over a specified axis.Common aggregate statistics incluse mean, median, or standard deviation.

We will also learn how to rearrange a DataFrame into a pivot table, which is a great way to compare data across two dimensions.

### Statistics

We will learn how to combine all of the values from a column for a single calculation.

For example:
- The DataFrame customers contains the names and ages of all of your customers. You want to find the median age:
```python
print(customers.age)
> [23, 25, 31, 35, 35, 46, 62]
print(customers.age.median())
> 35
```
- The DataFrame inventory contains a list of types of t-shirts that your company makes. You want a list of the colors that your shirts come in.
```python
print(inventory.color)
>> ['blue', 'blue', 'blue', 'blue', 'blue', 'green', 'green', 'orange', 'orange', 'orange']
print(inventory.color.unique())
>> ['blue', 'green', 'orange']
```

Command	Description:
mean	Average of all values in column
std	    Standard deviation
median	Median
max	    Maximum value in column
min	    Minimum value in column
count	Number of values in column
nunique	Number of unique values in column
unique	List of unique values in column

