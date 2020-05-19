# Pandas

### Mass setting some rows in pandas

```python
df.iloc[start_row:end_row,col_index] = 0
```

### Reset index

```python
# when groupby doesn't work (or when in doubt), reset index:
df.reset_index(inplace=True)
```

### Aggregate features

```python
# aggregate features (mainly count)
def add_aggregate_features(df, groupby_cols, aggregate_on, rename=None):
    '''
    groupby_cols is a list to group by
    aggregate_on dictionary, each entry is the kv pair column_name: aggregation (string, function, or list)
        rename is a dictionary of old names to new names
    '''
    all_cols = groupby_cols + list(aggregate_on.keys())
    group = df[all_cols].groupby([cols]).agg(aggregate_on).reset_index()
    group.columns = ['_'.join(col).strip() for col in group.columns.values]
    if rename:
        group.rename(index=str, columns=rename)
    df = df.merge(group, on=[groupby_cols], how='left')

def add_count(df, cols, target):
    colname = '_'.join(a) + '_count'
    add_aggregate_features(df, cols, {target: 'count'}, {target+"_count": colname})
```

### Another way to add count

```python
# Add counts by anttip
def df_add_counts(df, cols):
    arr_slice = df[cols].values
    unq, unqtags, counts = np.unique(np.ravel_multi_index(arr_slice.T, arr_slice.max(0) + 1),
                                     return_inverse=True, return_counts=True)
    df["_".join(cols)+'_count'] = counts[unqtags]

# Easier add count that doesn't require dummy column: 
df[group_cols].groupby(group_cols).size()
```

### Print a `groupby` object

```python
# printing a groupby object
def print_gp(gp):
    for key, item in gp:
        print(gp.get_group(key), "\n\n")
```



