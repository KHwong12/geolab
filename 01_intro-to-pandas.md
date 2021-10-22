---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.1'
      jupytext_version: 1.1.0
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

# Lab 01 - Introduction to pandas

**Author**: Kenneth Wong (khwongk12@gmail.com)
**Last Edited**: TODO

---

## Setup

```python
!pip3 install pandas geopandas
```

```python
import pandas as pd
import geopandas as gpd
```

---

learn how to **read and explore tabular data files in Python**. We will focus on using [pandas](https://pandas.pydata.org/pandas-docs/stable/) which is an open-source package for data analysis in Python. pandas is an excellent toolkit for working with **real world data** that often have a tabular structure (rows and columns).

We will first get familiar with the **pandas data structures**: *DataFrame* and *Series*:

![pandas data structures](https://geo-python-site.readthedocs.io/en/latest/_images/pandas-structures.png))

- **pandas DataFrame** (a 2-dimensional data structure) is used for storing and mainpulating table-like data (data with rows and columns) in Python. You can think of a pandas DataFrame as a programmable spreadsheet. 
- **pandas Series** (a 1-dimensional data structure) is used for storing and manipulating a sequence of values. pandas Series is kind of like a list, but more clever. One row or one column in a pandas DataFrame is actually a pandas Series. 

These pandas structures incorporate a number of things we've already encountered, such as indices, data stored in a collection, and data types. Let's have another look at the pandas data structures below with some additional annotation.

![pandas data structures annotated](https://geo-python-site.readthedocs.io/en/latest/_images/pandas-structures-annotated.png)

As you can see, both DataFrames and Series in pandas have an index that can be used to select values, but they also have column labels to identify columns in DataFrames. In the lesson this week we'll use many of these features to explore real-world data and learn some useful data analysis procedures.


## The dataset: weather statistics

Our input data is a text file containing weather observations from Kumpula, Helsinki, Finland retrieved from [NOAA](https://www.ncdc.noaa.gov/)*:

- File name: [Kumpula-June-2016-w-metadata.txt](Kumpula-June-2016-w-metadata.txt) (have a look at the file before reading it in using pandas!)
- The file is available in the binder and CSC notebook instances, under the L5 folder 
- The data file contains observed daily mean, minimum, and maximum temperatures from June 2016 recorded from the Kumpula weather observation station in Helsinki.
- There are 30 rows of data in this sample data set.
- The data has been derived from a data file of daily temperature measurments downloaded from [NOAA](https://www.ncdc.noaa.gov/cdo-web/).


## Reading a data file with pandas

Now we're ready to read in our temperature data file. **First, we need to import the pandas module.** It is customary to import pandas as `pd`:

```python
import pandas as pd
```

**Next, we'll read the input data file**, and store the contents of that file into a variable called `data` Using the `pandas.read_csv()` function:

```python
# Read the file using pandas
data = pd.read_csv('https://raw.githubusercontent.com/geo-python/site/master/source/notebooks/L5/Kumpula-June-2016-w-metadata.txt', skiprows = 8)
```

`pandas.read_csv()` is a general function for reading data files separated by commas, spaces, or other common separators. 

pandas has several different functions for parsing input data from different formats. There is, for example, a separate function for reading Excel files `read_excel`. Another useful function is `read_pickle` for reading data stored in the [Python pickle format](https://docs.python.org/3/library/pickle.html). Check out the [pandas documentation about input and output functions](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-tools-text-csv-hdf5) and Chapter 6 in [MacKinney (2017): Python for Data Analysis](https://geo-python-site.readthedocs.io/en/latest/course-info/resources.html#books) for more details about reading data.

If all goes as planned, you should now have a new variable `data` in memory that contains the input data. 

Let's check the the contents of this variable by calling `data` or `print(data)`:

```python
print(data)
```

After reading in the data, it is always good to check that everything went well by printing out the data as we did here. However, often it is enough to have a look at the top few rows of the data. 

We can use the `.head()` function of the pandas DataFrame object to quickly check the top rows. By default, the `.head()` function returns the first 5 rows of the DataFrame:

```python
data.head()
```

```python
data.tail()
```

Note that pandas DataFrames have **labelled axes (rows and columns)**. In our sample data, the rows labeled with an index value (`0` to `29`), and columns labelled `YEARMODA`, `TEMP`, `MAX`, and `MIN`. Later on, we will learn how to use these labels for selecting and updating subsets of the data.

Let's also confirm the data type of our data variable

```python
type(data)
```

No surprises here, our data variable is a pandas DataFrame.

---

## DataFrame properties

Let's continue with the full data set that we have stored in the variable `data` and explore it's contents further. 
A normal first step when you load new data is to explore the dataset a bit to understand how the data is structured, and what kind of values are stored in there.

### Length (number of rows/columns)

Let's start by checking the size of our data frame. We can use the `len()` function similar to the one we use with lists to check how many rows we have:

```python
# Check the number of rows 
len(data)
```

We can also get a quick sense of the size of the dataset using the `shape` attribute.

```python
# Check dataframe shape (number of rows, number of columns)
data.shape
```

Here we see that our dataset has 30 rows and 4 columns, just as we saw above when printing out the entire DataFrame.

`shape` is one of the several [attributes related to a pandas DataFrame](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html#attributes-and-underlying-data).

### Column Names

**We can also check the column names we have in our DataFrame.** We already saw the column names when we checked the 5 first rows using `data.head()`, but often it is useful to access the column names directly. You can check the column names by calling `data.columns` (returns an index object that contains the column labels) or `data.columns.values`:

```python
# Print column names
data.columns.values
```

We can also find information about the row identifiers using the `index` attribute:

```python
# Print index
data.index
```

Here we see how the data is indexed, starting at 0, ending at 30, and with an increment of 1 between each value. This is basically the same way in which Python lists are indexed, however, pandas also allows other ways of identifying the rows. DataFrame indices could, for example, be character strings, or date objects. We will learn more about resetting the index later.

What about the data types of each column in our DataFrame? We can check the data type of all columns at once using `pandas.DataFrame.dtypes`:

```python
# Print data types
data.dtypes
```

Here we see that `YEARMODA` is an integer value (with 64-bit precision; `int64`), while the other values are all decimal values with 64-bit precision (`float64`).

## Selecting columns

We can select specific columns based on the column values. The basic syntax is `dataframe[value]`, where value can be a single column name, or a list of column names. Let's start by selecting two columns, `'YEARMODA'` and `'TEMP'`:

```python
selection = data[['YEARMODA','TEMP']]
```

```python
selection
```

The subset is still a pandas DataFrame, and we are able to use all the methods and attributes related to a pandas DataFrame also with this subset. For example, we can check the shape:

```python
selection.shape
```

## Descriptive statistics

pandas DataFrames and Series contain useful methods for getting summary statistics. Available methods include `mean()`, `median()`, `min()`, `max()`, and `std()` (the standard deviation).

We could, for example, check the mean temperature in our input data. We check the mean for a single column (*Series*): 

```python
# Check mean value of a column
data['TEMP'].mean()
```

and for all columns (in the *DataFrame*):

```python
# Check mean value for all columns
data.mean()
```

For an overview of the basic statistics for all attributes in the data, we can use the `describe()` method:

```python
# Get descriptive statistics
data.describe()
```
