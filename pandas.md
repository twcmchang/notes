# Pandas

## Series
```
pd.Series(dict)             : dict "key" as index and "value" as value
pd.Series(data,index)       : can specify data and index
read_csv(..., squeeze=True) : convert DataFrame to Series by squeeze=True
```
- Attributes of Series
```
S.value
S.index
```
- Math Method in Series
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
D.value     : value, return nested array, list of array
D.shape     : return python tuple (n_row,n_col)
D.dtypes    : return dtype of every column 
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
- DateTime object in DataFrame
```
# using to_datetime function to convert into DateTime object
D['Date'] = pd.to_datetime(D['Date'])

# using 'parse_dates' in pd.read_csv()
D = pd.read_csv('filename.csv', parse_dates = ['Date1','Date2'])
```
- Filter by Boolean Series
```
# using Bool Series to access the rows whose is True, for example:
df[df['Team'] == "Finance"]

# using Bool Serier variable
mask = df['Start Date'] <= '2010-01-01'
df[mask]

# AND (&) , OR (|)
mask1 = df['Team'] == 'Finance'
mask2 = df['Team'] == 'Math'
df[mask1 | mask2]
```
- Filter by getting Boolean Series using methods
```
D['columnName'].isin(list)                      # return a Boolean Series that indicates whether an element in list
D['columnName'].isnull()                        # return a Boolean Series that indicates whether an element is null
D['columnName'].notnull()                       # the reverse of isnull()
D['columnName'].between(lower,upper)            # return a Boolean Series indicating whether an element between lower and upper
                                                # e.g. D['Login Time'].between('8:30AM','12:10PM') # example for DateTime object
                                                
D['columnName'].duplicated(subset,keep="last")  # return a Boolean Series indicating whether an element is duplicated
  - keep = "last", start searching from last row
  - subset = [], only consider the subset columns to find duplicates

D.drop_duplicates()                             # drop_duplicates() can be used on DataFrame not only Series
  - subset = [], 
  - keep = False,
  - inplace = True,
  
 D['columnName'].unique()                       # return an array of unique elements
 D['columnName'].nunique(dropna=True)           # return the number of unique elements (dropna default is True)
```
- Index
```
D.set_index(keys=["columnName"],inplace)        # set keys as index
D.reset_index(drop=false)                       # drop = True implies dropping current index
```
- Retrieve Rows by Index Label
```
# using Index Label
D.loc['index']      # return a Series whose key is composed of columns of D
D.loc['A':'Z']      # return a DataFrame includes 'Z' (***)

# using Index Location
D.iloc[2:4]         # return a DataFrame not includes 4

# using .ix method
D.ix[] works like D.loc[] but D.ix returns "not found error" as all null rows
D.ix[] works like D.iloc[] and both D.ix and D.iloc return "not found error"

# Second arguments to loc[], iloc[], ix[]
D.loc['index', ['columnName',...]]
D.iloc[rowIndex, [colIndex]]
D.ix['index',3], D.ix[3,['columnName']] all works
```
- Set New Value by ix[] method
```
D.ix['index',['C1','C2','C3']] = [V1,V2,V3]

# with another condition
D.ix[D['column1']=="T1", "column1"] = "New_T1"
```
- Rename Index Labels or Columns
```
D.rename(columns = {"ori_C1" : "new_C1", ...}, inplace = True)
D.rename(index = {"ori_I1" : "new_I1", ...}, inplace = True)

D.columns = ["new_C1", "new_C2", ...]
```
