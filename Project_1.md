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

A data frame is a two dimensional data structure in python - it can be pictured almost as a Microsoft Excel spreadsheet. Pandas is an incredibly useful package for work with data frames. In order to put data into a data frame, however, we must first import data by reading in a file from our computer. This can be done with pandas via the pandas.read_csv() function. In the code below, the first line imports pandas to use in our work session. The second sets the file path for pandas to use, and the third is a function to read in CSVs, or comma separated values files, as a data frame into our work session.

```
import pandas as pd 
path_to_data = 'C:/Users/Andrew/Desktop/COLLEGE STUFF/Spring 2021/Intro Data Science/Week 2/gapminder.tsv'
data = pd.read_csv(path_to_data, sep = '\t')
```

Notice that we added an argument in the last line of code (sep = "\t"). This is significant because we imported a .tsv file, or a tab seperated values file. The sep= argument is used to tell the computer what sort of character is seperating the values in our data. If we were to have used \c, the computer would look for commas to seperate the values and we would have an ugly mass of numbers and tabs. To make sure that we read in our data correctly, we can use a few functions. Below are two of those ways, the first of which will show us the top few rows of the dataset, and the second of which will show us how many rows and columns are in a data frame. 

```
data.head() #Shows the first 5 rows of our dataset

data.shape() #Shows the dimensions of the data frame, rows x columns 
```
Rows and columns can also be called called vectors. In my example, I imported the gapminder.tsv dataset. From our results, we can see the top five rows of our data and the dimensions of the data frame. The output looks like this:

```
>>>data.head()
       country continent  year  lifeExp       pop   gdpPercap
0  Afghanistan      Asia  1952   28.801   8425333  779.445314
1  Afghanistan      Asia  1957   30.332   9240934  820.853030
2  Afghanistan      Asia  1962   31.997  10267083  853.100710
3  Afghanistan      Asia  1967   34.020  11537966  836.197138
4  Afghanistan      Asia  1972   36.088  13079460  739.981106
>>>data.shape
(1704, 6)
```

## Question 3
##### Import the gapminder.tsv data set and create a new data frame. Interrogate and describe the year variable within the data frame you created. Does this variable exhibit regular intervals? If you were to add new outcomes to the raw data in order to update and make it more current, which years would you add to each subset of observations? Stretch goal: can you identify how many new outcomes in total you would be adding to your data frame?

In the above examples we already imported the gapminder.tsv dataset, though I will repeat the code here for posterity's sake. 

```
import pandas as pd 
path_to_data = 'C:/Users/Andrew/Desktop/COLLEGE STUFF/Spring 2021/Intro Data Science/Week 2/gapminder.tsv'
data = pd.read_csv(path_to_data, sep = '\t')
```

Let's take a look at the 'year' variable in our data frame. We can do this by subsetting the data frame and assigning the subset to an object, in case we want to do it later. Printing this object will also allow us to look at the column on its own. These things can be accomplished with the following (the output is included):

```
year_only = data['year']
year_only

>>>year_only
0       1952
1       1957
2       1962
3       1967
4       1972
        ... 
1699    1987
1700    1992
1701    1997
1702    2002
```
From the output, we can see that the column has regular intervals of 5 years. If we were to add more current data to our data frame, we would add 2007, 2012, 2017, and eventually 2022. 


## Question 4
##### Using the data frame you created by importing the gapminder.tsv data set, determine which country at what point in time had the lowest life expectancy. Conduct a cursory level investigation as to why this was the case and provide a brief explanation in support of your explanation.

To find what country had the lowest life expectancy, we can use the .min() function. By subsetting to only include the life expectancy column and using .min(), the computer will return the row with the lowest value for life expectancy. In the code below, we first find the column name that includes life expectancy, then use .min to find the value we are looking for. After we have found that value, we will subset the data frame for rows that include the value we found. The code chunk below includes the output for the last line of code.

```
data.columns
lifemin = data['lifeExp'].min()
#print(lifemin)
lowestlifeExp = (data['lifeExp'] == 23.599)
#print(lowestlifeExp)
temp = data[lowestlifeExp]
print(temp)

>>>print(temp)
     country continent  year  lifeExp      pop   gdpPercap
1292  Rwanda    Africa  1992   23.599  7290203  737.068595
```
Our output shows us that the country with the lowest life expectancy was Rwanda in 1992. This was likely due to the Rwandan Civil War (1990-1994) and ensuing Rwandan Genocide. Because our data was recorded in intervals of 5 years, the 1992 entry for Rwanda includes the years 1992-1996. The Rwandan Genocide occured in 1994 after the majority Hutu government ordered the killing of the minority Tutsi. The conflict led to the murder of up to 800,000 Rwandans, which for the purposes of our analysis clearly explains why the life expectancy in Rwanda was so low at that time.

## Question 5
##### Using the data frame you created by importing the gapminder.tsv data set, multiply the variable pop by the variable gdpPercap and assign the results to a newly created variable. Then subset and order from highest to lowest the results for Germany, France, Italy and Spain in 2007. Create a table that illustrates your results (you are welcome to either create a table in markdown or plot/save in PyCharm and upload the image). Stretch goal: which of the four European countries exhibited the most significant increase in total gross domestic product during the previous 5-year period (to 2007)?





