## ENH: Support reduction methods on Index #50021
```py
In[1]: import pandas as pd

# Create a numeric Index
In[2]: index = pd.Index([3,4,5,6,7])

# Perform reduction methods
In[3]: index.kurt()
Out[3]:
-1.2000000000000002

In[4]: index.skew()
Out[4]:
0.0

In[5]: index.sem()
Out[5]:
0.7071067811865476

# sem() also supports the optional parameter ddof (default ddof=1)
In[6]: index.sem(ddof=2)
Out[6]:
0.816496580927726

In[7]: index.count()
Out[7]:
5

In[8]: index.sum()
Out[8]:
25

In[9]: index.product()
Out[9]:
2520

In[10]: index.mean()
Out[10]:
5.0

In[11]: index.median()
Out[11]:
5.0

# std() and var() also support the optional parameter ddof (default ddof=1)
In[12]: index.std(ddof=2)
Out[12]:
1.8257418583505538

In[13]: index.var()
Out[13]:
2.5
```

## ENH: Allow easy selection of ordered/unordered categorical columns #46941
```py
IN[1]: import pandas as pd

# create a DataFrame with four columns
IN[2]: df = pd.DataFrame({"ordered": [1, 2, 3, 4], "randomBool": [True, False] * 2, "unordered": ["red", "blue", "green", "yellow"], "randomInt": [1]*4})

# create an ordered categorical column
IN[3]: ordered_categories = [1, 2, 3, 4]
IN[4]: df["ordered"] = pd.Categorical(df["ordered"], ordered_categories, ordered=True)

# create an unordered categorical column
IN[5]: unordered_categories = ["red", "blue", "green", "yellow"]
IN[6]: df["unordered"] = pd.Categorical(df["unordered"], unordered_categories, ordered=False)

# verify 
IN[7]: df
Out[7]: 
   ordered  randomBool unordered  randomInt
0        1        True       red          1
1        2       False      blue          1
2        3        True     green          1
3        4       False    yellow          1
IN[8]: df.dtypes
OUT[8]:
ordered       category
randomBool        bool
unordered     category
randomInt        int64
dtype: object

# use select_dtypes() to select only ordered category
IN[9]: df.select_dtypes(include='category', ordered=True)
OUT[9]:
  ordered
0       1
1       2
2       3
3       4

# use select_dtypes() to exclude only unordered category
IN[10]: df.select_dtypes(exclude='category', ordered=False)
OUT[10]:
  ordered  randomBool  randomInt
0       1        True          1
1       2       False          1
2       3        True          1
3       4       False          1

# use select_dtypes() to include int and only ordered category
IN[11]: df.select_dtypes(include=['int', 'category'], ordered=True)
OUT[11]:
  ordered  randomInt
0       1          1
1       2          1
2       3          1
3       4          1

# use select_dtypes() to exclude bool and only ordered category
IN[12]: df.select_dtypes(exclude=['bool', 'category'], ordered=True)
OUT[12]:
  unordered  randomInt
0       red          1
1      blue          1
2     green          1
3    yellow          1

# use select_dtypes() to include bool and all category
IN[13]: df.select_dtypes(include=['bool', 'category'])
OUT[13]:
  ordered  randomBool unordered
0       1        True       red
1       2       False      blue
2       3        True     green
3       4       False    yellow

# use DataFrame's cat attribute to select only category
IN[14]: df.cat.select_categories()
OUT[14]:
  ordered unordered
0       1       red
1       2      blue
2       3     green
3       4    yellow

# use DataFrame's cat attribute to select only ordered category
IN[15]: df.cat.select_ordered_categories()
OUT[15]:
  ordered
0       1
1       2
2       3
3       4

# use DataFrame's cat attribute to select only ordered category
IN[16]: df.cat.select_unordered_categories()
OUT[16]:
  unordered
0       red
1      blue
2     green
3    yellow

# use DataFrame's cat attribute to check whether each column is category
IN[17]: df.cat.is_category()
OUT[17]:
[True, False, True, False]

# use DataFrame's cat attribute to check whether each column is ordered category
IN[18]: df.cat.is_ordered()
OUT[18]:
[True, <NA>, False, <NA>]
```
