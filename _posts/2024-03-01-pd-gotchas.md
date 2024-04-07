# Gotchas in Pandas

1. TOC
{:toc}

## Concat when series names are incosistent
When one concats a dictionary of series' with different name, the name is set to None. While if all series' are same, then name is preserved
```
d1 = {'a': pd.Series([1,2], name="id"),'b': pd.Series([2,3],name="id2")}
print(pd.concat(d1, axis="rows"))

d1 = {'a': pd.Series([1,2], name="id"),'b': pd.Series([2,3],name="id")}
print(pd.concat(d1, axis="rows"))
```
![](/images/pdgt1.png "Series name preserved")
