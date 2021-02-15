# Project 1

This project involves 10 questions on the basics of python, dataset manipulation, and pandas. 

## Question 1
##### Describe what is a package? Also, describe what is a library? What are the two steps you need to execute in order to install a package and then make that library of functions accessible to your workspace and current python work session? Provide examples of how you would execute these two steps using two of the packages we have used in class thus far. Be sure to include an alias in at least one of your two examples and explain why it is a good idea to do so.

In python, a package is a directory of modules (a module is a collection of functions). A library is a collection of related functions that can be called with the name of the library followed by a period. Pandas is an example of a library. To install a package in Pycharm, you can click on settings, then 'Python Interpreter'. Then press the plus sign at the bottom of the page, type in the package you are looking for, and install it. 

The next step is to import the library to make the functions usable in your workspace. Below are two examples of how to import packages. The first imports the package os, which we used to check if a folder already existed on our computer. Using import followed by the package will make it usable by its full name. In the second example, I imported the package pandas and gave it an alias with the code 'as pd'. 
```
import os

import pandas as pd
```
In our workspace, we can now reference the pandas package by simply using pd. The alias makes it simpler to reference the package and generally takes very little time to do - it is therefore recommended that you give your packages an alias when importing them.


## Question 2
##### Describe what is a data frame? Identify a library of functions that is particularly useful for working with data frames. In order to read a file in its remote location within the file system of your operating system, which command would you use? Provide an example of how to read a file and import it into your work session in order to create a new data frame. Also, describe why specifying an argument within a read_() function can be significant. Does data that is saved as a file in a different type of format require a particular argument in order for a data frame to be successfully imported? Also, provide an example that describes a data frame you created. How do you determine how many rows and columns are in a data frame? Is there an alternate terminology for describing rows and columns?
