---
layout: post
title: Data Understanding
image: "/posts/data-understanding-img.png"
tags: [Data Mining Pipeline, Data Understanding, Python]
---

In this post, I’ll walk through a Python function that quickly calculates key statistics for dataset attributes, offering valuable insights into the data. Then, I will build a function to generate a scatter plot using Matplotlib to visually explore the dataset and uncover further insights.
<br>

# Table of contents

- [00. Data Understanding Overview](#data-understanding-overview)
  - [Context](#data-understanding-context)
  - [Actions](#data-understanding-actions)
  - [Results](#data-understanding-results)
  - [Tests](#data-understanding-tests)
- [01. Data Visualization Overview](#data-visualization-overview)
  - [Context](#data-visualization-context)
  - [Actions](#data-visualization-actions)
  - [Results](#data-visualization-results)
  - [Tests](#data-visualization-tests)

---

# Data Understanding Overview <a name="data-understanding-overview"></a>

### Context <a name="data-understanding-context"></a>

There are 5 steps in Data Mining Pipeline:

- Data understanding
- Data pre-processing
- Data warehousing
- Data modeling
- Pattern evaluation
  <br>

I will cover Data Understanding in this post and explore:

- Data objects & attributes
- Data statistics
- Data visualization
- Data similarity

The fisrt function to be defined should return the following attributes for the ith column:

- Number of objects
- The minimum value
- The maximum value
- The mean value
- The standard deviation value
- The Q1 value
- The median value
- The Q3 value
- The IQR value

<br>
<br>
### Actions <a name="data-understanding-actions"></a>

- Import the required Python packages & libraries

```python
# import required Python packages and libraries
import argparse
import pandas as pd
import numpy as np
import pickle
from pathlib import Path
```

- Define the function to calculate and return statistics on those attributes

```python
# define the calculate function
def calculate(dataFile, col_num):
    """
    Input Parameters:
        dataFile: The dataset file.
        ithAttre: The ith attribute for which the various properties must be calculated.

    Default value of 0,infinity,-infinity are assigned to all the variables as required.
    """
    numObj, minValue, maxValue, mean, stdev, Q1, median, Q3, IQR = [0,"inf","-inf",0,0,0,0,0,0]

    #load the dataset
    data = pd.read_csv(dataFile)

    #select attribute
    attre_selection = data.iloc[:, col_num]

    #calculate stats
    numObj = attre_selection.count()
    minValue = attre_selection.min()
    maxValue = attre_selection.max()
    mean =  attre_selection.mean()
    stdev =  attre_selection.std()
    Q1 = attre_selection.quantile(0.25)
    median = attre_selection.median()
    Q3 = attre_selection.quantile(0.75)
    IQR = Q3 - Q1

    #return results
    return numObj, minValue, maxValue, mean, stdev, Q1, median, Q3, IQR
```

<br>
<br>
### Tests <a name="data-understanding-tests"></a>

- Run tests using unittest
  The _unittest_ library is a built-in Python library used for writing and running tests for your code.
  It provides a framework to create unit tests, which are small and focused tests designed to check if individual pieves of your code (such as functions and methods) work correctly.

```python
# import required Python packages and libraries
import unittest

# define the test cases / assertions
class TestKnn(unittest.TestCase):
    def setUp(self):
        self.loc = "/Users/cintiacampos/CUBoulder/Data_Mining/pipeline_data/dataset.csv"
        file = open('/Users/cintiacampos/CUBoulder/Data_Mining/pipeline_data/testing', 'rb')
        self.data = pickle.load(file)
        file.close()

    def test0(self):
        """
        Test the label counter
        """
        self.column = self.data[0]
        result = calculate(self.loc,self.column)
        self.assertEqual(result[0],self.data[1][0])
        self.assertAlmostEqual(result[1],self.data[1][1], places = 3)
        self.assertAlmostEqual(result[2],self.data[1][2], places = 3)
        self.assertAlmostEqual(result[3],self.data[1][3], places = 3)
        self.assertAlmostEqual(result[4],self.data[1][4], places = 3)
        self.assertAlmostEqual(result[5],self.data[1][5], places = 3)
        self.assertAlmostEqual(result[6],self.data[1][6], places = 3)
        self.assertAlmostEqual(result[7],self.data[1][7], places = 3)
        self.assertAlmostEqual(result[8],self.data[1][8], places = 3)

tests = TestKnn()
tests_to_run = unittest.TestLoader().loadTestsFromModule(tests)
unittest.TextTestRunner().run(tests_to_run)
```

<br>
<br>

### Results <a name="data-understanding-results"></a>

Tests returned 0 errors and 0 failures indicating that the functions above were defined correctly.

<unittest.runner.TextTestResult run=1 errors=0 failures=0>

<br>
<br>

---

# Data Visualization Overview <a name="data-visualization-overview"></a>

In this part, I will generate a scatter plot and explore the data visually.
The function should:

<br>
<be>

### Actions <a name="data-visualization-actions"></a>

- Import Python packages and libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

- Define the function where:
  - Initialize an empty list for x and for y
  - Initialize title, x-label, and y-label as empty strings
  - Load the dataset
  - Extract x and y values from the data
  - Define Title and Labels
  - Return x, y, title, x_label, y_label
    <br>
    <br>

```python
def func():

    '''
        Output: x, y, title, x-label, y-label
    '''
    x = []
    y = []
    title = ''
    x_label = ''
    y_label = ''

    #load the dataset
    data = pd.read_csv('/Users/cintiacampos/CUBoulder/Data_Mining/pipeline_data/dataset.csv')

    # Extract x and y values
    x = data['CO'].tolist()
    y = data['AFDP'].tolist()

    # Define Titles and Labels
    title = 'CO vs AFDP'
    x_label = 'CO'
    y_label = 'AFDP'

    return x, y, title, x_label, y_label
```

### Results <a name="data-visualization-results"></a>

[placeholder]

<br>
<be>

### Tests <a name="data-visualization-tests"></a>

```python
from IPython.display import Image, display
# Display the image with a custom size
display(Image(filename='/Users/cintiacampos/CUBoulder/Data_Mining/pipeline_data/week3_data/scatter_plot.png', width=300, height=200))
```

```python
# Testing the func() function
x, y, title, x_label, y_label = func()
plt.scatter(x, y)
plt.title(title)
plt.xlabel(x_label)
plt.ylabel(y_label)
```

<br>
<br>
