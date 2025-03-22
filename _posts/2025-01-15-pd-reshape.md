# 3 Lesser known pandas function for data transformation


1. TOC
{:toc}

## Inverse of pivot
pandas.lreshape

```
data = pd.DataFrame({'hr1': [514, 573], 'hr2': [545, 526],
                     'team': ['Red Sox', 'Yankees'],
                     'year1': [2007, 2007], 'year2': [2008, 2008]})
data
   hr1  hr2     team  year1  year2
0  514  545  Red Sox   2007   2008
1  573  526  Yankees   2007   2008

pd.lreshape(data, groups = {'year': ['year1', 'year2'], 'hr': ['hr1', 'hr2']})
      team  year   hr
0  Red Sox  2007  514
1  Yankees  2007  573
2  Red Sox  2008  545
3  Yankees  2008  526

```

## Unpivot
pandas.wide_to_long

```
np.random.seed(123)
df = pd.DataFrame({"A1970" : {0 : "a", 1 : "b", 2 : "c"},
                   "A1980" : {0 : "d", 1 : "e", 2 : "f"},
                   "B1970" : {0 : 2.5, 1 : 1.2, 2 : .7},
                   "B1980" : {0 : 3.2, 1 : 1.3, 2 : .1},
                   "X"     : dict(zip(range(3), np.random.randn(3)))
                  })
df["id"] = df.index
df
  A1970 A1980  B1970  B1980         X  id
0     a     d    2.5    3.2 -1.085631   0
1     b     e    1.2    1.3  0.997345   1
2     c     f    0.7    0.1  0.282978   2
pd.wide_to_long(df, ["A", "B"], i="id", j="year")

                X  A    B
id year
0  1970 -1.085631  a  2.5
1  1970  0.997345  b  1.2
2  1970  0.282978  c  0.7
0  1980 -1.085631  d  3.2
1  1980  0.997345  e  1.3
2  1980  0.282978  f  0.1

```

## Inverse of dummy encoding 
pandas.from_dummies
```
df = pd.DataFrame({"a": [1, 0, 0, 1], "b": [0, 1, 0, 0],
                   "c": [0, 0, 1, 0]})
df
   a  b  c
0  1  0  0
1  0  1  0
2  0  0  1
3  1  0  0

pd.from_dummies(df)
0     a
1     b
2     c
3     a

```

<!-- ## Categorical Encoding
pandas.factorize
differ from numpy.unique in handling nans
```
values = np.array([1, 2, 1, np.nan])
codes, uniques = pd.factorize(values)  # default: use_na_sentinel=True
codes
array([ 0,  1,  0, -1])
uniques
array([1., 2.])

codes, uniques = pd.factorize(values, use_na_sentinel=False)
codes
array([0, 1, 0, 2])
uniques
array([ 1.,  2., nan])

``` -->
