# Pandas

## Series
```
pd.Series(dict)               # dict "key" as index and "value" as value
pd.Series(data,index)         # can specify data and index
read_csv(..., squeeze=True)   # convert DataFrame to Series by squeeze=True
```
- Attributes of Series
```
S.value
S.index
```
- Math Method in Series
```
S.count()                           # number of elements
S.sum()                             # summation of elements (numeric)
S.mean()                            # mean
S.std()                             # standard deviation
S.min()                             # minimum
S.max()                             # maximum
S.median()                          # median
S.mode()                            # most frequent element
S.describe()                        # return count,mean,std,min,25%,50%,75%,max
S.idxmax()                          # the index of maximal element
S.idxmin()                          # the index of minimal element
S.value_counts(ascending=False)     # counts by value
S.apply(custom_function)            # for every element in Series, do custom_function
S.map(arg)                          # map value of S to index of arg, find the corresponding value in arg
                                    # and return the mapping back, where arg can be another Series or an dictionary
```

## DataFrame
- Shared attributes and methods with Series
```
D.head(n_row)     # the first several rows (default=5)
D.tail(n_row)     # the last several rows (default=5)
D.index           # attribute
D.value           # value, return nested array, list of array
D.shape           # return python tuple (n_row,n_col)
D.dtypes          # return dtype of every column 
```
- Special for DataFrame
```
D.columns               # Index([column names])
D.axes                  # [X_object, Column_object]
D.info()                # summary of DataFrame
D.get_dtype_counts()    # the counts of each dtype
D.nunique()             # number of unique elements
```
- Difference between Shared Methods
```
D.sum(axis=0)           # column-wise summation 
D.sum(axis=1)           # or axis="columns"row-wise summation # one is vertical line
```
- Extract single column from DataFrame
```
D.columnName                # return Series; if columnName contains any space, it doesn't work
D["columnName"]             # more safe
D[extCol]                   # extCol = ["C1","C2","C3"] to select multiple columns
```
- Add new column from DataFrame
```
D['new_column_name'] = 'new column'                            # automatically repeat to all Series
D.insert(loc,column='new_column_name',value=new_column_value)  # loc = column index to insert
```
- Broadcast
```
 D['numeric'].add(5)                                           # equal to D['numeric'] + 5, for +,-,*,/
```
- Drop or Fill
```
D.dropna(axis=0, how='all', inplace=True) 
  - axis                        # axis = 0 or "row", axis = 1 or "column";
  - how = 'any'                 # remove that have any null values at all
  - how = 'all'                 # remove that all of values are equal to null
  - inplace = True              # True for overwrite the called DataFrame
  - subset = ['considered']     # remove that have any null values in subset columns

D.fillna(value) 
  - inplace = True              # True for overwrite the called DataFrame
```
- astype() # convert data type in Series
```
D['columnName'] = D['columnName'].astype('int')
D['columnName'] = D['category'].astype('category') # convert into different categories to reduce memory usage
```
- Sort a DataFrame
```
D.sort_values(by,axis,ascending,inplace,na_position=False)
  - by = ['C1','C2',...]            # ordered columns used to sort by 
  - ascending = [True, False]       # can be selected by True or False
  - axis = {0,1}                    # according to row or column
  - inplace = True                  # True for overwrite the called DataFrame
  - na_position = 'last'            # or 'first'

D.sort_index(ascending,inplace)

D['rank'] = D.rank()                # return a ranking Series
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
D.loc['index']          # return a Series whose key is composed of columns of D
D.loc['A':'Z']          # return a DataFrame includes 'Z' (***)

# using Index Location
D.iloc[2:4]             # return a DataFrame not includes 4

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
- Drop Rows or Columnsin DataFrame
```
D.drop(["Index1",...], inplace = True)    # remove rows whose index in ["Index1",...]
D.drop(["C1",...], axis = 'column')       # 
D.pop("C1")                               # pop out a column, C1, from D and return a Series 
del D["C1"]                               # delete "C1" column
```
- Create Random Sample
```
D.sample(n=5, axis=0)             # sample 5 rows of D
D.sample(frac = .25, axis=0)      # sample 25% of rows in D
```
- nsamllest or nlargest
```
D.nlargest(n=5, columns="C1")     # sort by "C1" column and select the largest n=5
D.nsmallest(n=5, columns="C2")    # sort by "C2" column and select the smallest n=5

# it is similar to
D.sort_values("C1").head(5)
```
- where
```
D.where(condition)                # return a full DataFrame but only the rows met the condition have values and the others are all NaNs
```
- query
```
D.query("condition")              # return subset of DataFrame contains all rows met the condition
                                  # condition is a string
```
- .apply() method on Single Columns
```
D["C1"] = D["C1"].apply(function_to_do)  # apply function_to_do on every element of column "C1"
```
- .apply() method with Row Values
```
D.apply(function_to_do, axis = "columns") # axis = "columns" implies the function_to_do executes over columns,
                                          # so it iterates over rows
```
- .copy method to create exact copy
```
D.copy()      # exact copy to anoteher memory space
```

### Text Data in DataFrame
```
## Something Different
D["C1"].str.lower()
D["C1"].str.upper()
D["C1"].str.title()
D["C1"].str.replace("match","replace")  # replace "match" by "replace"
D["C1"].str.contains("match")           # return a Boolean Series
D["C1"].str.startswith("match")         # return a Boolean Series that strings in "C1" start with "match"
D["C1"].str.endswith("match")           # return a Boolean Series that strings in "C1" end with "match"
D["C1"].str.lstrip()                    # strip the space at left end
D["C1"].str.rstrip()                    # strip the space at right end
D["C1"].str.strip()                     # strip off at both ends

## can revise Index and Columns by string method
D.index = D.index.str.strip()
D.columns = D.columns.str.title()

## split strings by " " and get the first element as title
D["C1"].str.split(" ").str.get(0).str.title()

## str.split("split",expand = True)
# >> will return a DataFrame not a list
D[["First Name","Last Name"]] = D["Name"].str.split(",",expand=True)

## str.split(..., expand = True, n = 1)
# >> n=1 means that max split is set to 1 
D["title"].str.split("split", expand=True, n = 2)
```
### Multi-index
```
D.set_index(["C1","C2"])            #
D.index                             # would be MultiIndex(levels = [[ c1,...], [c2,...]])
D.index[0]                          # would get a tuple (C1[0],C2[0])

D.index.get_level_values(0)         # D["C1"], equal to D.index.get_level_values("C1")
D.index.get_level_values(1)         # D["C2"]

D.index.set_names(["new_C1","new_C2"])    # change Index name, and use inplace=True

D.sort_index(ascending = True)            # all index in ascending order
D.sort_index(ascending = [True,False])    # first index in acsending order, second indx in descending order

```
- Extract rows from MultiIndex DataFrame
```
D.loc[("C_11")]               # extract the rows whose first index == "C11"
D.loc[("C_11","C_21"),"V_1"]  # extract the first index == "C11" and second index == "C21" and get "V1"'s value
```
### Method
```
D.transpose()                     # swap axes
D.ix["V_1",("C_11","C_21")]

D.swaplevel(i=-2,j=-1)            # swap level i to j , and j to i

D.stack()                         # stack all columns of a DataFrame into a Series by Index
D.stack().to_frame()              # back to DataFrame => 1 column of value

D.unstack()                       # go to the most inner (the most dense cell) layer to the column axis
D.unstack(level = 2)              # unstack the level = 2 layer into columns, or by name
D.unstack(level = [1,0], fill=0)  # unstack multiple levels layer in order to columns

# generate/aggregate a condensed DataFrame from a DataFrame
D.pivot(index="column_as_index",
        columns="column_to_be_expanded",
        values="column_as_value")

# pivot table
D.pivot_table(values="column_as_value",             # can be a list, MultiIndex
              index="column_as_index_to_group",     # can be a list, MultiIndex
              aggfunc='mean')                       # "sum", "mean", "max", "min"     

# pd.melt()
pd.melt(D,
        id_vars = "Index",                          # column "Index" as index variable
        var_name="var_n",                           # new variable name
        value_name="val_n")                         # new value name
```
