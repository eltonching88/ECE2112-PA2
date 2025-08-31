<h1 align="center"> ECE2112 Programming Assignment 2 (Numpy) </h1>

<a id="top"></a>

## Table of Contents
### 1. [Normalization Problem](#anchor-normalization)
### 2. [Divisible by 3 Problem](#anchor-divby3)
<br/>

<a name="anchor-normalization"></a>
## **I. Normalization Problem**
* Normalization is one of the most basic preprocessing techniques in data analytics. This involves centering and scaling process. Centering means subtracting the data from the mean and scaling means dividing with its standard deviation. Mathematically, normalization can be expressed as:

* ###  $`Z = \frac{X - x}{σ}`$

* In Python, element-wise mean and element-wise standard deviation can be obtained by using `.mean()` and `.std()` calls.
In this problem, create a random 5 x 5 ndarray and store it to variable X. Normalize X. Save your normalized ndarray as X_normalized.npy


**Step 1.** Before coding with ndarrays, we must import the numpy library.
``` python
import numpy as np
```
<br/>

**Step 2.** I used  `np.random.random()` to generate a 5x5 matrix with randomized values.
``` python
# A 5x5 array with randomized values
X = np.random.random( (5,5) ) 
```
<br/>

**Step 3.** Using the provided syntaxes `.mean()` and `.std()` and the given formula, I stored the normalized values in a new array `X_normalized`. Translating the formula into Python, the mean array `X.mean()` is first subtracted from the original array `X`, then it is divided by the standard deviation array `X.std()`. Lastly, we save the data using `.save()`, which downloads the array as a .npy file.
``` python
# Using the formula and code providedx
X_normalized = (X - X.mean()) / X.std()
np.save("X_normalized.npy", X_normalized)
```
<br/>

**Step 4.** To view the matrix data, we can simply print the array.
```python
# To check the values,
print("Random Values:\n", X, "\n")                       # Show randomized values
print("Normalized Values:\n", X_normalized, "\n")        # Show normalized values
print("Stored Values:\n", np.load("X_normalized.npy"))   # Check if file saved normalized data
```
<br/>

**Possible Output**: 
``` 
Random Values:
 [[0.71162792 0.20285693 0.96377271 0.58634068 0.63386418]
 [0.4211127  0.43549484 0.37744306 0.08403909 0.39110762]
 [0.76780722 0.13662081 0.85001822 0.73867995 0.26595706]
 [0.37701478 0.95272832 0.47323084 0.008879   0.26127026]
 [0.2018807  0.52753741 0.69288635 0.27549455 0.31115795]] 

Normalized Values:
 [[ 0.93533203 -1.00165717  1.89529586  0.45833937  0.63927051]
 [-0.17071538 -0.1159598  -0.33697413 -1.45401957 -0.2849505 ]
 [ 1.14921746 -1.25383083  1.46221059  1.03832435 -0.7614228 ]
 [-0.33860467  1.85324772  0.02770841 -1.74016851 -0.77926635]
 [-1.00537385  0.23446401  0.86397929 -0.72511175 -0.58933431]] 

Stored Values:
 [[ 0.93533203 -1.00165717  1.89529586  0.45833937  0.63927051]
 [-0.17071538 -0.1159598  -0.33697413 -1.45401957 -0.2849505 ]
 [ 1.14921746 -1.25383083  1.46221059  1.03832435 -0.7614228 ]
 [-0.33860467  1.85324772  0.02770841 -1.74016851 -0.77926635]
 [-1.00537385  0.23446401  0.86397929 -0.72511175 -0.58933431]]
```

<br/>


<a name="anchor-divby3"></a>
## **II. Divisible by 3 Problem**
* Create a 10 x 10 ndarray, which is the squares of the first 100 positive integers. From this ndarray, determine all the elements that are divisible by 3. Save the result as div_by_3.npy.


**Step 1.** Again, we must import the numpy library first.
``` python
import numpy as np
```
<br/>

**Step 2.** I created a 10x10 array filled with 1's as a placeholder for the values. I also specified the array's data type `dtype=np.int16` since it sometimes returns float values.
``` python
# Create a 10x10 filled with 1's
X = np.ones([10,10],dtype=np.int16) # Specified dtype due to float output
```
<br/>

**Step 3.** To assign values one by one, I used two for loops. The first loop starts at the first row and waits for the second loop to go through each column. The `col` loop assigns the squared value of n, which increments by 1 each iteration.
``` python
n = 1
for row in range(10):     # Loop through rows 
    for col in range(10): # Loop through cols
        X[row,col] = n**2 # Square the value per column
        n += 1            # Increase n value by 1
```
<br/>

**Step 4.** I created a new array `div` to store only the values divisible by 3. By using modulo (%) on the original array, it takes each value and divides it by 3. If the remainder is 0, then the value is stored in `div`. Lastly, we save the new array data in "div_by_3.npy" by using `.save()`.
``` python
div = X [X%3 == 0]           # Store values divisible by 3
np.save("div_by_3.npy", div) # Save values
```
<br/>

**Step 5.** I printed out the values to verify the results.
``` python
print("10x10 Matrix:\n", X, "\n")                   # Show matrix data
print("Divisible by 3:\n",div, "\n")                # Show values divisible by 3
print("Saved Values:\n", np.load("div_by_3.npy"))   # Check if file saved div data
```
<br/>

**Expected Output**: 
``` 
10x10 Matrix:
 [[    1     4     9    16    25    36    49    64    81   100]
 [  121   144   169   196   225   256   289   324   361   400]
 [  441   484   529   576   625   676   729   784   841   900]
 [  961  1024  1089  1156  1225  1296  1369  1444  1521  1600]
 [ 1681  1764  1849  1936  2025  2116  2209  2304  2401  2500]
 [ 2601  2704  2809  2916  3025  3136  3249  3364  3481  3600]
 [ 3721  3844  3969  4096  4225  4356  4489  4624  4761  4900]
 [ 5041  5184  5329  5476  5625  5776  5929  6084  6241  6400]
 [ 6561  6724  6889  7056  7225  7396  7569  7744  7921  8100]
 [ 8281  8464  8649  8836  9025  9216  9409  9604  9801 10000]] 

Divisible by 3:
 [   9   36   81  144  225  324  441  576  729  900 1089 1296 1521 1764
 2025 2304 2601 2916 3249 3600 3969 4356 4761 5184 5625 6084 6561 7056
 7569 8100 8649 9216 9801] 

Saved Values:
 [   9   36   81  144  225  324  441  576  729  900 1089 1296 1521 1764
 2025 2304 2601 2916 3249 3600 3969 4356 4761 5184 5625 6084 6561 7056
 7569 8100 8649 9216 9801]
```

<br/>
<br/>

**Author**: Elton Ching (2ECE-B)


**Nothing follows. Thank you for reading!** 

<p align="right"> (<a href="#top">Back to Top</a>) </p>
