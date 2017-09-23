# Pandas

## Series
```
pd.Series(dict)             : dict "key" as index and "value" as value
pd.Series(data,index)       : can specify data and index
read_csv(..., squeeze=True) : convert DataFrame to Series by squeeze=True
```

### Attributes of Series
```
S.value
S.index
```

### Math Method in Series
```
S.count(): number of elements
S.sum()  : summation of elements (numeric)
S.mean() : mean
S.std()  : standard deviation
S.min()  : minimum
S.max()  : maximum
S.median()  : median
S.mode()    : most frequent element
S.describe(): count,mean,std,min,25%,50%,75%,max
S.idxmax()  : the index of maximal element
S.idxmin()  : the index of minimal element
S.value_counts(ascending=False): counts by value
S.apply(custom_function)  : for every element in Series, do custom_function
S.map(arg)  : map value of S to index of arg and find the corresponding value in arg, and return the mapping back
               - arg can be another Series or an dictionary
```

## DataFrame
- Shared attributes and methods with Series
```
D.head(n_row) : the first several rows (default=5)
D.tail(n_row) : the last several rows (default=5)
D.index     : attribute
D.value     : value (return nested array, list of array)
D.shape     : python tuple (n_row,n_col)
D.dtypes    : dtype of every column 
```

- Special for DataFrame
```
D.columns   : Index([column names])
D.axes      : [X_object, Column_object]
D.info()    : summary of DataFrame
D.get_dtype_counts() :  the counts of each dtype
```
- Difference between Shared Methods
```
D.sum(axis=0)  : column-wise summation 
D.sum(axis=1 or axis="columns")  : row-wise summation # one is vertical line
```
