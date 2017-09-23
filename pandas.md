## Series
pd.Series(dict) where dict: "key" as index and "value" as value
pd.Series()
read_csv(...,squeeze=True): convert DataFrame to Series by squeeze=True

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
