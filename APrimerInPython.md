# A very short primer in Python
Author
: Thomas Block, Bonn University, tmblock@physik.uni-bonn.de

Before we jump into some of the main functionalities of the Python language, it has to be mentioned, that all features and packages, which are presented below, are extremely well documented on the internet (original documentation, stackoverflow etc.).  This paper just exist to give you a first idea what Python can (or cannot) do and to direct you where you can begin to look for, when something is not working or you want to expand your knowledge.

## 1		Structure of code
Blocks of code, which belong together, have the same level of indentation, usually measured in tabulator space or four spaces (instead of using brackets like in C/C++).  Commands, like function calls, assignments, etc., are separated from each other by a new line (instead of usually semi-colons). If you want to comment out lines use hashes (#) at the beginning of the line and for commenting out multiple lines at once, enclose the lines with a pair of triple quotes:

```python
# This line is commented out

'''
The whole area enclosed in two
triple-quotes are commented out.
Very nice!
'''
```

## 2		Lists

Lists are the "standard-arrays" of the Python language.  They can contain objects of any type (e.g. integers, floats, strings, functions, objects of classes).  Lists can be assigned to a variable name like:

```python
# Define me a little list
my_list = [1, 1, 2, 3, 5, 8, 13]
```

Following basic gymnastics can be done on lists:

- ```len(my_list)```: Returns the amount of elements of a list (in our example the value would be ```7```)
- ```my_list[2]```: Returns the third element of the list (in our example ```2```)
- ```my_list[start:stop:step]```: Returns elements starting from index *start* to index *stop* in steps of *step*. For example ```my_list[1:6:2]``` would return ```[1,3,8]```

There are shorthand notation for the last indexing method. When ```step``` is not specified, it is set to 1 by default. When ```start``` and\or ```stop``` is not specified, it is set to 0 or rather ```len(my_list)```.
 
- ```my_list[:3]```: Returns the first three elements of the list ```[1, 1, 2]```
-  ```my_list[3:]```: Returns all elements but the first three elements ```(3, 5, 8, 13]```

List of lists are also possible.  They resemble multi-dimensional arrays and the elements are accessed accordingly, for example:

```python
my_other_list = [[1, 2, 3, 4], [5, 6, 7, 8]]
```
- ```my_other_list[1][3]```: Returns the fourth element of the second list (8)


## 3		Functions
It is always useful to define functions as we don't want to repeat lines of code, which do basically the same thing.  Let's define a linear function with a slope $a$ and intersect $b$, which returns and prints the result:

```python
def linear_func(x, a, b):
    print(a*x + b)
    return a*x + b
```

Note, that the list of parameters are now in round brackets and the declaration ends with a colon.  Function calls with the same result (result1 = result2 = 5) look like this:

```python
result1 = linear_func(1, 2, 3)
result2 = linear_func(a=2, b=3, x=1)

Output:
5
5
```

We can therefore choose the order of our parameters in the function calls by explicit assignment of the values to the parameters.

## 4		Control structures

### for-loop
For iterating over a range of elements we can use

```python
for i in range(len(my_list)):
    print(i, my_list[i])
    
Output:
0, 1
1, 1
2, 2
3, 3
4, 5
5, 8
6, 13
```

 The *range*-statement in this case creates a list of integers between 0 and *len(my\_list)* and sets for each loop *i* to the subsequent element of the list. We can also loop over all elements of a list:
```python
for name in ['cat', 'mouse', 'dog', 'bird']:
	print(name)

Output:
cat
mouse
dog
bird
```

### while-loop

Sometimes we have to wait for a condition to be fulfilled until we want the program to be resumed.  Here we can use while-loops.  In this example the elements will be printed out until the elements are larger than 5 (using the list from above):

```python
i = 0
while my_list[i] < 6:
    print(my_list[i])
    i = i + 1
    
Output:
1
1
2
3
5
```
### conditional statements
 Conditional statements can be used like this:

```python
a = 3
b = 4

if a < b:
    print('b is larger than a')
elif a > b:
    print('a is larger than b')
else:
    print('a and b are the same')
    
Output:
'b is larger than a'
```

Note that text is enclosed in quotes (double-quotes are also possible, but choose one type of quotation for consistency).


## 5		*numpy* 

*numpy* stands for 'numerical python' and provides structures and functions for fast numerical evaluations and should be used instead of standard lists.  *numpy* generates 'real' arrays. Here a neat functions from the *numpy*-package:

- ```my_array = numpy.array([[1,2],[3,4]])``` Creates a 2D array of the name *my_array*
- ```my_array = numpy.linspace(0,9,10)``` Creates an array of ten evenly spaced values between 0 and 9 of the name *my_array*
- ```numpy.loadtxt``` Loads a formatted text file into numpy arrays.  For example if *file.txt* looks like this:
```python
x,y
0.2,0.4
0.4,0.8
0.6,1.6
0.8,3.2
```
we can load the file like this:
```python
import numpy as np

data = np.loadtxt('file.txt', delimiter= ',',
			      usecols = (0,1), skiprows = 1)
print(data)

Output:
[[0.2 0.4]
 [0.4 0.8]
 [0.6 1.6]
 [0.8 3.2]]
```
- We want to be also able to save results from calculations.  Lets save two lists to a text file:
```python
import numpy as np

a = [1, 2, 3, 4]
b = [5, 6, 7, 8]
# Save the lists with 4 digits after the comma
np.savetxt('saveddata.txt', (x,y), delimiter=',', fmt = '%.4f')
```
*saveddata.txt* should then look like this:
```
1.0000,2.0000,3.0000,4.0000
5.0000,6.0000,7.0000,8.0000
```

### Indexing and data selection
Very similar to lists we can access elements, or even whole subsets, of an array. Consider a 3x3 two-dimensional array:
```
my_array = np.array([[1,3,5],[2,4,7],[3,6,9]])
```
- ```my_array[0]``` selects the first array (or first row). Output:  ``` [1,3,5]```
- ```my_array[1, 2]``` selects the third element of the second array. Output: ```7```
- ```my_array[:, 1]``` selects from all arrays the second element (or the second column). Output: ```[3,4,6]```

## 6		Plotting with *matplotlib*

*matplotlib* is a Python package, which provides a lot of useful functions and services for visualizing data. Here I will show some examples how to work with it:

### Plotting of 2D data

As straightforward as it gets:
``` python
# Import package and give it an alias
import matplotlib.pyplot as plt

# Set up some dummy data
# Note: The amount of elements have to match
x_coord = [1, 2, 4, 6, 8, 10]
y_coord = [1, 4, 16, 36, 64, 100]

plt.figure(figsize = (5, 3.5), dpi = 200) # Create figure to draw in
plt.xlabel('time in s')                   # Set label for x-axis
plt.ylabel('position in m')               # Set label for y_axis
plt.title('My plot')                      # Set title of plot 
plt.grid(True)                            # Show grid
# Plot data, 'bo' means 'blue (b) circles (o)'
plt.plot(x_coord, y_coord, fmt = 'bo' label = 'Data points')
plt.legend() # Print out label
# Save plot in directory of running notebook
plt.savefig('myfirstplot.pdf')
```

### Plotting of 2D data with errorbars
We can also include errorbars, if we have uncertainties on our data sample:

```python
import matplotlib.pyplot as plt

x_coord = [1, 2, 4, 6, 8, 10]
y_coord = [1, 4, 16, 36, 64, 100]
x_err   = [.1, .2, .4, .6, .8, 1.0]
y_err   = [.1, .4, 1.6, 3.6, 6.4, 10.0]

plt.figure(figsize = (5, 3.5), dpi = 200)
plt.xlabel('time in s')
plt.ylabel('position in m')
plt.title('My plot')
plt.grid(True)
plt.errorbar(x_coord, y_coord, xerr = x_err, yerr = y_err,
             label='Datapoints with errorbars', fmt = 'gx')
plt.legend()
plt.savefig('myfirstplotwitherrorbars.pdf')
```
Note: The plotting function changed to *errorbar*

### Plotting a function
Sometimes we want to compare data sets to models and analytical functions.  Plotting functions in *matplotlib* is not so intuitive, because we have to generate the function values as our y-coordinates first. To give the illusion of a smooth curve we have to generate many data points:

```python
import matplotlib.pyplot as plt
import numpy as np

def quad_curve(x, a, b):
    return (a-x)**2 + b

# create 1001 data points
x_coord = np.linspace(0, 10, 1001)
y_coord = quad_curve(x_coord, 1, 2)

plt.figure(figsize = (5, 3.5), dpi = 200) 
plt.xlabel('x coordinate')                
plt.ylabel('y coordinate')                
plt.title('My plot')                       
plt.grid(True)                            

plt.plot(x_coord, y_coord, 'bo', label = 'Data points',
		markersize = 1)
plt.legend() # Print out label

plt.savefig('myfirstplotwithafunction.pdf')
```

> Note here one crucial advantage of *numpy*-arrays versus lists: If we wanted to create data points with a list, the creation of the y-coordinates would have required a for-loop over all elements in the list of x-coordinates. *numpy*-arrays executes an operation for all elements in the array automatically and returns an array with the same amount of elements. 
