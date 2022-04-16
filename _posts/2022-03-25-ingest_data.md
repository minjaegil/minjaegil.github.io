---
layout: single
title: "Data Ingestion using Pandas"
categories: Python
tag: [pandas, data science, python]
toc: true
toc_sticky: true
toc_label: "Contents"
use_math: true
---

## Flat Files (CSV)

### Specifying Delimiters

When reading `tsv` (tab-separated variables) files, we need to specify the delimiter with `sep`. 

```python
import pandas as pd

data = pd.read_csv("some_data.tsv", sep="\t")
```

### Limiting Columns

Choose columns to load with the `usecols` keyword argument.

```python
col_names = ['STATEFIPS', 'STATE', 'zipcode', 'agi_stub', 'N1']
col_nums = [0, 1, 2, 3, 4]

# Choose columns to load by name
tax_data_v1 = pd.read_csv('us_tax_data_2016.csv', usecols=col_names)

# Choose columns to load by number
tax_data_v2 = pd.read_csv('us_tax_data_2016.csv',usecols=col_nums)
```

### Limiting Rows

Limit the number of rows loaded with the `nrows` keyword argument.

```python
data_first1000 = pd.read_csv('some_data.csv', nrows=1000)
```

Use `skiprows` to skip rows. `skiprows` accepts a list of row numbers, a number of rows, or a function to filter rows.

```python
data_next500 = pd.read_csv('some_data csv', 
                            nrows=500, 
                            skiprows=1000, 
                            header=None)
```
Set `header=None` when there are no column names.

### Setting Data Types

Dictionary types can be passed in `na_values` and `dtype`.

```python
data = pd.read_csv("some_data_.csv",                        
                    na_values={"column1" : 0}
                    dtype={"column2": str})
```

### Handling Errors

Set `error_bad_lines=False` to skip unparseable records.

Set `warn_bad_lines=True` to see messages when records are skipped.

```python
data = pd.read_csv("some_data.csv", 
                    error_bad_lines=False, 
                    warn_bad_lines=True)
```

