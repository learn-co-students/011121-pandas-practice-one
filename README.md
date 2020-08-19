# Pandas 101

This checkpoint contains many of the basic tasks you might need to do with Pandas!  At the end of an hour, commit and push what you have (remember, you can always return to this book later for practice)


```python
# Run this import cell without changes

#data manipulation
import pandas as pd

#dataset
from sklearn.datasets import load_boston
```

## Loading in the Boston Housing Dataset


```python
# Run this cell without changes
boston = load_boston()
```

The variable `boston` is now a dictionary with several key-value pairs containing different aspects of the Boston Housing dataset.  

#### What are the keys to `boston`?  

Assign the keys the variable `boston_keys`


```python
### BEGIN SOLUTION


from test_scripts.test_class import Test
test = Test()

boston_keys = boston.keys()

test.save(len(boston_keys), 'boston_keys_len')

### END SOLUTION
```


```python
### BEGIN HIDDEN TESTS

test_keys = boston.keys()



try:
    boston_keys
except NameError:
    raise AssertionError ("Looks like 'boston_keys' wasn't assigned an object?")

    
    
assert type(boston_keys) == type(test_keys), "Looks like there's a different type of object than dict_keys?"
    

    
test.run_test(len(boston_keys),
              "boston_keys_len",
              "Looks like you have the wrong number of keys?"
             )



assert test_keys == boston_keys, "Looks like you assigned the wrong object to 'boston_keys'?"



### END HIDDEN TESTS
```

#### Use the print command to print out the metadata for the dataset contained in the key `DESCR`


```python
#your code here
```

#### Create a dataframe named `df_boston` with data contained in the key `data`.  

#### Make the column names of `df_boston` the values from the key `feature_names`


```python
### BEGIN SOLUTION

    
df_boston = pd.DataFrame(boston['data'], columns=boston['feature_names'])

df_boston.reindex(sorted(df_boston.columns), axis=1)
df_boston.sort_values('CRIM', ascending=False, inplace=True)

test.save(type(df_boston), 'df_boston_type')
test.save(len(df_boston), 'df_boston_len')
test.save(df_boston, 'df_boston')


### END SOLUTION
```


```python
### BEGIN HIDDEN TESTS

try:
    df_boston.reindex(sorted(df_boston.columns), axis=1)
    df_boston.sort_values('CRIM', ascending=False, inplace=True)
except NameError:
    raise AssertionError ("Looks like 'df_boston' isn't a dataframe?")


test.run_test(type(df_boston), 
              'df_boston_type',
             "Looks like 'df_boston' isn't a dataframe?"
             )

test.run_test(len(df_boston), 
              'df_boston_len',
              "Looks like the dataframe is the wrong length?"
             )

test.run_test(df_boston, 
              'df_boston',
              "Looks like the dataframe isn't what it should be?"
             )

### END HIDDEN TESTS
```

The key `target` contains the median value of a house.  

#### Add a column named "MEDV" to `df_boston` which contains the median value of a house


```python
### BEGIN SOLUTION


df_boston['MEDV'] = boston['target']

df_boston.reindex(sorted(df_boston.columns), axis=1)
df_boston.sort_values('CRIM', ascending=False, inplace=True)

test.save(df_boston, 'df_boston')



### END SOLUTION
```


```python
### BEGIN HIDDEN TESTS


try:
    df_boston.reindex(sorted(df_boston.columns), axis=1)
    df_boston.sort_values('CRIM', ascending=False, inplace=True)
except NameError:
    raise AssertionError ("Looks like 'df_boston' isn't a dataframe?")

test.run_test(df_boston, 'df_boston', "looks like the column wasn't added correctly?")


### END HIDDEN TESTS
```

## Data Exploration

#### Show the first 5 rows of the dataframe with the `head` method


```python
#your code here
```

#### Show the summary statistics of all columns with the `describe` method


```python
#your code here
```

#### Check the datatypes of all columns, and see how many nulls are in each column, using the `info` method


```python
#your code here
```

## Data Selection

#### Select all values from the column that contains the weighted distances to five Boston employment centres

#### Assign this series to the variable `distances` 

*Hint: you printed out the information about what information variables contain in a cell above*


```python
### BEGIN SOLUTION

distances = df_boston['DIS']

distances = distances.sort_values(ascending=False, kind='mergesort')

test.save(len(distances), 'distances_len')
test.save(list(distances.index),'distances_index')
test.save(list(distances.values), 'distances_values')

### END SOLUTION
```


```python
### BEGIN HIDDEN TESTS

try:
    distances = df_boston['DIS']
    distances = distances.sort_values(ascending=False, kind='mergesort')
    
except NameError:
    raise AssertionError ("Looks like `distances` isn't assigned anything?")

test.run_test(len(distances),
              'distances_len',
              "Looks like you have the wrong number of values?"
             
             )

test.run_test(list(distances.index),
             "distances_index",
              "Looks like you have the wrong index?"
             )

test.run_test(list(distances.values),
             "distances_values",
              "Looks like you have the wrong values?"
             )


### END HIDDEN TESTS
```

#### Select rows 10-20 from the AGE, NOX, and MEDV columns

#### Assign them to the variable `age_nox_medv`


```python
### BEGIN SOLUTION

age_nox_medv = df_boston.loc[10:20, ['AGE', 'NOX', 'MEDV']]

age_nox_medv.reindex(sorted(age_nox_medv.columns), axis=1)
age_nox_medv.sort_values('AGE', ascending=False, inplace=True)

test.save(age_nox_medv, 'age_nox_medv')


### END SOLUTION
```


```python
### BEGIN HIDDEN TESTS

try:
    age_nox_medv.reindex(sorted(age_nox_medv.columns), axis=1)
    age_nox_medv.sort_values('AGE', ascending=False, inplace=True)
except NameError:
    raise AssertionError ("Looks like `age_nox_medv` isn't assigned anything?")

test.run_test(age_nox_medv,
              'age_nox_medv',
              "Looks like the wrong data was assigned?"
             )

### END HIDDEN TESTS
```

#### Select all rows where NOX is greater than .7 and CRIM is greater than 8

#### Assign those rows the variable `nox_crim`


```python
### BEGIN SOLUTION

mask = (
    (df_boston['NOX']>.7) &
    (df_boston['CRIM']>8)
)

nox_crim = df_boston[mask]

nox_crim.reindex(sorted(nox_crim.columns), axis=1)
nox_crim.sort_values('NOX', ascending=False, inplace=True)

test.save(nox_crim, 'nox_crim')



### END SOLUTION
```

    /Users/benoren/opt/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:11: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      # This is added back by InteractiveShellApp.init_path()



```python
### BEGIN HIDDEN TESTS

try:
    nox_crim.reindex(sorted(nox_crim.columns), axis=1)
    nox_crim.sort_values('AGE', ascending=False, inplace=True)
    
except NameError:
    raise AssertionError ("Looks like `nox_crim` isn't assigned anything?")


test.run_test(nox_crim,
              "nox_crim",
              "Looks like the wrong data was assigned?"
             )


### END HIDDEN TESTS
```

    /Users/benoren/opt/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:5: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      """


## Data Manipulation

#### Add a column to the dataframe called "MEDV*TAX" which is the product of MEDV and TAX


```python
### BEGIN SOLUTION

df_boston['MEDV*TAX'] = df_boston['MEDV']*df_boston['TAX']

df_boston.reindex(sorted(df_boston.columns), axis=1)
df_boston.sort_values('AGE', ascending=False, inplace=True)

test.save(df_boston, 'df_boston_medvtax')


### END SOLUTION
```


```python
### BEGIN HIDDEN TESTS

try:
    df_boston.reindex(sorted(df_boston.columns), axis=1)
    df_boston.sort_values('AGE', ascending=False, inplace=True)
except NameError:
    raise AssertionError ("Looks like `df_boston` isn't assigned anything?")

test.run_test(df_boston,
              'df_boston_medvtax',
              "Looks like the wrong data was added?"
             )


### END HIDDEN TESTS
```

#### What is the average median value of houses located on the Charles River?

#### Assign your end calculation to the variable `val`


```python
### BEGIN SOLUTION


val = (
    df_boston
    [df_boston['CHAS']==1]
    ['MEDV']
    .mean()
)

val = val*1000
val

test.save(val, 'val')



### END SOLUTION
```


```python
### BEGIN HIDDEN TESTS

import math

if not math.isclose(val, test.load_ind('val'), rel_tol=.1):
    raise AssertionError ("Looks like you have the wrong calculation?")

### END HIDDEN TESTS
```

#### Write a sentence that answers the above question

=== BEGIN MARK SCHEME ===



'''The average median value of houses located along the Charles River is $28,440'''

=== END MARK SCHEME ===
