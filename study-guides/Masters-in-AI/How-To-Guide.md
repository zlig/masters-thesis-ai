# How To Guide

## Exploratory Data analysis (EDA) Phase

* Understand data
* Select feature(s)
* Run sample tests with various options, parameters and models types
* Execute large scale model training

## Definitions

* [Validations Assumptions and Identify Patterns](https://www.svds.com/value-exploratory-data-analysis/)

## Pandas
### Load dataset

* [Technical Notes and Common Operations](https://chrisalbon.com/)

```
# Import libraries
import numpy as np
from pandas import read_csv
import matplotlib.pyplot as plt

# Read data from file
dataframe = read_csv("dataset.csv")  # Option: header=None if the first row is containing data

# Show the first 5 rows
dataframe.head(5)

# Display number or rows and columns in set
dataframe.shape

# Display type of columns
dataframe.dtypes

# Display statistics of dataframe
#   Option: include='<types>' if needing to display statistics for only some data types
dataframe.describe(include='all')
```

```
# Extract comuns with only numerical data
numerical_columns = dataframe.describe().columns
print(numerical_columns)
```

```
# Extract comuns with only categorical data
categorical_columns = dataframe.select_dtypes(include=['category', object]).columns
print(categorical_columns)
```

```
# Create an identical copy of dataframe (for experiments)
dataframe_copy = dataframe.copy(deep=True)
```

### Working Missing Values

Rarely datasets are available already cleansed and prepared, with a common issue being to have missing values from the rows.

The following commands are helping to solve those:
```
# Drop the columns where all elements are missing values:
df.dropna(axis=1, how='all')

# Drop the columns where any of the elements are missing values
df.dropna(axis=1, how='any')

# Keep only the rows which contain 2 missing values maximum
df.dropna(thresh=2)

# Drop the columns where any of the elements are missing values
df.dropna(axis=1, how='any')

# Fill all missing values with the mean of the particular column
df.fillna(df.mean())

# Fill any missing value in column 'A' with the column median
df['A'].fillna(df['A'].median())

# Fill any missing value in column 'Depeche' with the column mode
df['Depeche'].fillna(df['Depeche'].mode())
```

```
# List data with missing values for particular column
df[df['Depeche'].isnull()]
```

```
# Conditionally impute values
df.loc[(df['age'] > 50) & (df['age'] <= 65), 'age_group'] = 'senior'
```

```
# Reset indexes after dropping NaNs values
df.dropna(inplace=True)
df.reset_index(drop=True, inplace=True)
```



## Numpy

### Array Manipulations

```
# View 10 first rows
X[:10,:]

# View 10 first rows
y[:10]

# View first column only
X[:,[0]]

# View 10 first rows of the first column only
X[:10,[0]]

# View 10 first rows of the second column only
X[:10,[1]]

# Square experiment on the first 10 rows of the first column
X[:10,[0]]**2
```

```
# Experimenting to create X2 = (x1,x2,x1^2,x2^2)
X2 = X
x1_squared = X[:,[0]]**2
x2_squared = X[:,[1]]**2
X2 = np.append(X, x1_squared, 1)
X2 = np.append(X2, x2_squared, 1)
X2.shape
```

## Create Plots

* [What plots?](https://towardsdatascience.com/what-plot-why-this-plot-and-why-not-9508a0cb35ea)
* [Visualisation using Pandas](https://machinelearningmastery.com/visualize-machine-learning-data-python-pandas/)
