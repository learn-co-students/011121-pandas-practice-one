# Pandas 101

This checkpoint contains many of the basic tasks you might need to do with Pandas!  At the end of an hour, commit and push what you have.  Then you can keep working on this later if you want to


```python
# Run this cell without changes
import pandas as pd
from sklearn.datasets import load_boston
```

### Loading in the Boston Housing Dataset


```python
# Run this cell without changes
boston = load_boston()
```

### Print out the metadata for the dataset contained in 'DESCR'


```python

```

### Assign the data and feature_names to variables


```python

```

### Create a dataframe with the array ```features``` and the correct column names


```python

```

### Add a MEDV column to your dataframe using the values from target


```python

```

### Look at the first 5 rows of the dataframe


```python

```

### Show summary statistics of all rows


```python

```

### Check if there are null values and the datatypes of all columns using the info method


```python

```

### Select the % lower status of the population column


```python

```

### Select rows 10-20 from the AGE, NOX, and MEDV columns


```python

```

### Select all values from the INDUS column with a proportion of non-retail business acres per town less than 2


```python

```

### Select all rows where NOX is greater than .7 and CRIM is greater than 8


```python

```

### Add a column called ONES to the dataframe which consists of all 1s


```python

```

### Add a column to the dataframe called MEDV_times_TAX which is the product of MEDV and TAX


```python

```

### What is the average MEDV of houses located on the Charles River


```python


#28.44
```


```python

```
