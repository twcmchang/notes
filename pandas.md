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
D.nunique() : number of unique elements
```
- Difference between Shared Methods
```
D.sum(axis=0)  : column-wise summation 
D.sum(axis=1 or axis="columns")  : row-wise summation # one is vertical line
```
- Extract single column from DataFrame
```
1.  D.columnName    # return Series; if columnName contains any space, it doesn't work
2.  D["columnName"] # more safe
3.  extCol = ["C1","C2","C3"]
    D[extCol] # select multiple columns
```
- Add new column from DataFrame
```
D['new_column_name'] = 'new column' # automatically repeat to
D.insert(loc,column='new_column_name',value=new_column_value)  # loc = column index to insert

- Broadcast
 D['numeric'].add(5) # equal to D['numeric'] + 5, for +,-,*,/
```
- Drop or Fill
```
D.dropna(axis=0, how='all', inplace=True) 
  - axis                    # axis = 0 or "row", axis = 1 or "column";
  - how = 'any'             # remove that have any null values at all
  - how = 'all'             # remove that all of values are equal to null
  - inplace = True          # True for overwrite the called DataFrame
  - subset = ['considered'] # remove that have any null values in subset columns

D.fillna(value) 
  - inplace = True           True for overwrite the called DataFrame
```
- astype() # convert data type in Series
```
D['columnName'] = D['columnName'].astype('int')
D['columnName'] = D['category'].astype('category') # convert into different categories to reduce memory usage
```
- Sort a DataFrame
```
D.sort_values(by,axis,ascending,inplace,na_position=False)
  - by = ['C1','C2',...]           # ordered columns used to sort by 
  - ascending = [True, False, ...] # can be selected by True or False
  - axis
  - inplace = True                 # True for overwrite the called DataFrame
  - na_position = 'last'           # or 'first'

D.sort_index(ascending,inplace)

D['rank'] = D.rank()  # return a ranking Series
```
