# Introduction to Apache Spark #
## February 5, 2019 ##
## Adam Miller ##

### Spark and the Data Science Cycle ###
  - In the context of data science, Spark helps with:
    - Data understanding/prep
    - Modeling
    - Evaluation
    - Deployment
   - It can transform data and clean it non-destructively
### Spark vs. Hadoop ###
  - Spark's main advantage over Hadoop is that it can keep its intermediate results in short term memory (RAM)
  - RAM bandwidth has increased exponentially over time when compared to that of regular hard drives
### Spark Libraries ###
  - *ML*: Machine learning library
  - *Spark Streaming*: Library built for high throughput and high fault tolerance **(class won't focus on this)**
  - *Spark SQL*: Library for processing SQL queries in-memory
  - *GraphX*: Graph API for analytics **(class won't focus on this)**
### Spark v1.6 and Spark v2.0 ###
  - 1.6 is generally good for cleaning data, while 2.0 is better for analytics/modeling
  - 1.6 uses **RDDs** (Resilient Distributed Databases), while 2.0 uses a **DataFrame** structure (similar to R and SQL)
  - Newer versions of Spark use **DataSet**, which is a statically-typed dataframe (more structure than a DataFrame)
### Spark MapReduce Examples ###
*Create spark session*
```python
from pyspark.sql import SparkSession
# Spark 2.0+
spark = SparkSession.builder.getOrCreate()
# Spark 1.6 (RDDs)
sc = spark.sparkContext
```
#### Example 1 (Shakespeare Data) ####
```python
# Pull 'Shakespeare' text data and filter for the word 'love' #
shakespeare = sc.textFile("/datasets/shakespeare.txt")
love = shakespeare.filter(lambda x: 'love' in x.lower())

# Count the number values in 'love and time it #
%timeit love.count()

# Cache the 'love' variable in memory, then count the number of values again, and time it #
love.cache()
%timeit love.count()
```

#### Example 2 (Monthly Order Data) ####
```python
# Create dataset, then create an RDD for that dataset #
example_dataset = [
['JAN', 'NY', 3.],
['JAN', 'PA', 1.],
['JAN', 'NJ', 2.],
['JAN', 'CT', 4.],
['FEB', 'PA', 1.],
['FEB', 'NJ', 1.],
['FEB', 'NY', 2.],
['FEB', 'VT', 1.],
['MAR', 'NJ', 2.],
['MAR', 'NY', 1.],
['MAR', 'VT', 2.],
['MAR', 'PA', 3.]]

dataset_rdd = sc.parallelize(example_dataset)

# Define map function #
def map_func(row):
    return [row[0], row[2]]
    
# Take first five elements and map them #
dataset_rdd.map(map_func).take(5)

# Define the reduce function to find the number of orders per month #
def reduce_func(value1, value2):
  return value1 + value2

# Reduce the mapped intermediate pairs #
dataset_rdd.map(map_func).reduceByKey(reduce_func).collect()

# Repeat for average monthly orders #
def avg_map_func(row):
  return [row[0], row[2]]

def avg_reduce_func(value1, value2):
  return (value1 + value2)/2
 
dataset_rdd.map(avg_map_func).reduceByKey(avg_reduce_func).collect()
```

### Transformations ###
  - `map(func)`: returns a new distributed dataset formed by passing each element of the source through the function *func*.
  - `flatMap(func)`: same as `map` but when multiple key-value pairs are returned.
  - `filter(func)`: return a new dataset formed by selecting those elements of the source on which *func* returns true. 
  - `reduceByKey(func)`: when called on a dataset of (K, V) pairs, returns a dataset of (K, V) pairs where the values for each key are aggregated using the given reduce function *func*.
  - `sortByKey([ascending],[numTasks])`: when called on a dataset of (K, V) pairs where K implements `Ordered`, returns a dataset of (K, V) pairs sorted by keys in ascending or descending order, as specified in the Boolean **ascending** argument.
  - `join(otherDataset, [numTasks])`: when called on datasets of type (K, V) and (K, W), returns a dataset of (K, (V, W)) pairs with all pairs of elements for each key.
  - `distinct([numTasks])`: returns a new dataset that contains the distinct elements of the source dataset.
  - `pipe(command, [envVars])`: pipes each partition of the RDD through the provided shell *command*.

#### Transformations Example ####
```python
neg_values = dist_array.map(lambda x: x-1)
print("neg_values", neg_values.collect())
large_values = dist_array.filter(lambda y: y > 10)
print("large_values", large_values.collect())
```
### Actions ###
- `reduce(func`): Aggregate the elements of the dataset using a function *func* (which takes two arguments and returns one). The function should be commutative and associative so that it can be computed correctly in parallel.
- `foreach(func)`: Runs the function *func* on each element in the dataset.
- `count()`: returns the number of elements in the dataset.
- `first()`: returns the first element in the dataset.
- `take(n)`: returns an array with the first ***n*** elements of the dataset.
- `saveAsTextFile(path)`: writes the elements in the dataset out to a file in HDFS (or some other file system.)
- `saveAsSequenceFile(path)`: writes the elements to HDFS in the `SequenceFile` format.

### Using Spark for Word Count ###
*Shakespeare Example:*
```python
'''
Transform shakespeare dataset, and divide words into a corpus.  Then map each word using an anonymous function,
and reduce the intermediate pairs by summing them in order to find the number of times each word appears
'''

wordCounts = shakespeare.flatMap(lambda line: line.lower().split()).\
    map(lambda word: (word, 1)).\
    reduceByKey(lambda a, b: a + b).\
    sortBy(lambda x: -x[1])
wordCounts.take(10)
```
### Join Operations on RDDs ###
  - Join operations combine two sets of data by computing the **Cartesian Product** between two sets (i.e. two RDDs)
  - **Left join** keeps values in the left dataset, and **right join** is vice-versa
  - Used as filters to improve performance
  
### Spark 2.0 and DataFrames ###
  - RDDs do not have enough structure, and are slower/harder to optimize.
  - DataFrames are structured as a distributed collection of data with named columns
  - "Pandas for big data"
  - Can read from multiple sources:
    - **Parquet** files are one preferred source (datasets stored in columns)
    - Column storage is preferred because data is all one type; easier for processing/compression
  - Can read from python row objects, RDDs, and files (i.e. .csv)
  - Once the DataFrame is created, **python is no longer used**; commands are now specialized
### Operations with Spark DataFrames ### 
  - select, modify, filter, join, group, and aggregate
  - Can also show the scheme of the DataFrame by using `printSchema()`
  - Operations are symbolic, meaning they hold *literal* values, and *placeholder* columns
  - Some operations can't take strings, only accept a literal or placeholder as a value (i.e. Exponents)
  - Some operations (`fn.sum`, `fn.stddev`, `fn.count`, `fn.countdistinct`) only work on grouped data; applied using `agg(operation)`
  - Can sample from DataFrame and output result as Pandas using `.sample`, can also perform random number generation using `spark.range`
    - **Important to have training, testing, and validating datasets when sampling**
#### DataFrame Example ####
```python
# Import 'functions' Spark module #
from pyspark.sql import functions as fn

# Create locations data as a python row object #
locations_df = spark.createDataFrame([
    Row(location_id = 'loc1', n_employees=3, state='NY'),
    Row(location_id = 'loc2', n_employees=8, state='NY'),
    Row(location_id = 'loc3', n_employees=3, state='PA'),
    Row(location_id = 'loc4', n_employees=1, state='FL')    
])

# Read the data into a spark DataFrame #
transactions_df = spark.createDataFrame([
    Row(transaction_id = 1, location_id = 'loc1', n_orders=2.),
    Row(transaction_id = 2, location_id = 'loc1', n_orders=3.),
    Row(transaction_id = 3, location_id = 'loc3', n_orders=5.),
    Row(transaction_id = 4, location_id = 'loc5', n_orders=5.)
])

# Use a symbolic operation to show the number of employees + 1 #
locations_df.select(1 + fn.col('n_employees')).show(10)

# Change column name/type #
new_column = 1+fn.col('n_employees')
locations_df.select(new_columns.alias('new_columns')).show(10)
locations_df.select(new_columns.alias('new_column.alias('new_column').cast('float')).show(10)
```





  
  
  
  
  
  
  
  
  
  

