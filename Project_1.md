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

Below is the table I created after going through the steps outlined in the question. I have not added the code here as I believe the output shows my work, but would be happy to do so if needed!

 Country       | Continent          | Year  |Life Expectancy     | Population   | GDP per Capita  |GDP  |
|:-------------:|:-------------:|:-----:|:-------------:|:-------------:|:-----:|:-----:|
| Germany| Europe | 2007| 79.406 | 82400996 | 32170.37442 | 2.650871e+12 |
| France | Europe | 2007 | 80.657 | 61083916  | 30470.01670 | 1.861228e+12 |
| Italy | Europe | 2007 | 80.546 | 58147733 | 28569.71970 | 1.661264e+12 |
| Spain | Europe | 2007 | 80.941 | 40448191 | 28821.06370 | 1.165760e+12 |

## Question 6
##### You have been introduced to four logical operators thus far: &, ==, | and ^. Describe each one including its purpose and function. Provide an example of how each might be used in the context of programming.

In python, &, ==, | and ^ are called bitwise operators. We will use them as logical operators in boolean logic, though they also serve another function with numbers by treating them as binary code (I looked a bit into this but am not familiar with binary code). Let's go through them one by one.

& is the bitwise form of AND. It will look at two conditions and output TRUE if both conditions it is considering are true. This can be used in conjunction with things like 'if' statements to make code run only if certain conditions are met. In the example below, the code would print "Not all are 4" because the '&' will only run the 'if' line if BOTH a and b are equal to 4. They are not both equal to 4, so the computer runs the 'else' statement's code.

```
a = 5
b = 4

if a & b == 4:
    print("Both are 4")
else:
    print("Not all are 4")
```

| is the bitwise form of OR. OR will look at two conditions and output TRUE if either condition it is considering is true. We can adapt the code snippet we just ran to see how it functions in code. The below code is the same as the snippet above, except in the 'if' statement the '&' has been replaced with a '|' and the printed statements have been adapted to fit our new operator. Now the computer is looking for EITHER a or b to be equal to 4. Because 'b' is equal to 4, running the code will return "One is 4" because one of our objects is equal to 4.

```
a = 5
b = 4

if a | b == 4:
    print("One is 4")
else:
    print("Neither are 4")
```

== means 'equal to' in python, and will return True if the operands on both sides of it are equal. We can continue to use the same code snippet to demonstrate how it functions. In the 3rd line of the below code, we use == to tell the computer that both a and b must be equal (hence the ==) to 4 in order for the statement to be true. We cannot use '=' because that is used to assign things to objects.

```
a = 5
b = 4

if a & b == 4: #This line showcases the use of '=='
    print("Both are 4")
else:
    print("Not all are 4")
```

^ is a bitwise operator called "exclusive or". It compares two bits, and for each bit that is the same, outputs a 0. If the bits are different, it will output a 1. We can use the integers 6 and 3 to demonstrate how this functions. In binary, 6 is equivalent to 110 while 3 is equivalent to 011. In the first bit, the bits are different, so we get a 1. In the second bit, they are the same, and in the third they are different, giving us 01. Put all of those together and you get 101, or binary for 5. Let's take a look at the code and it's output.

```
x = 6 ^ 3
print(x)

>>>5
```

## Question 7
##### Describe the difference between .loc and .iloc. Provide an example of how to extract a series of consecutive observations from a data frame. Stretch goal: provide an example of how to extract all observations from a series of consecutive columns. 

.loc and .iloc allow you to filter out parts of a dataframe based on the name of their row or column, or based on their index. .loc will filter out rows or columns based on their label names. On the other hand, .iloc will filter out rows or columns based on their integer locations. We can use either to extract a series of consecutive observations from a data frame. For example, lets say we wanted to extract only the 2nd - 6th rows in our data frame. Because we are using the index as the means of subsetting, we will use .iloc. This is shown in the below code snippet and output following it. 

```
subset = data.iloc[2:6]
print(subset)

>>>iloc
       country continent  year  lifeExp       pop   gdpPercap
2  Afghanistan      Asia  1962   31.997  10267083  853.100710
3  Afghanistan      Asia  1967   34.020  11537966  836.197138
4  Afghanistan      Asia  1972   36.088  13079460  739.981106
5  Afghanistan      Asia  1977   38.438  14880372  786.113360
```

## Question 8
##### Describe how an api works. Provide an example of how to construct a request to a remote server in order to pull data, write it to a local file and then import it to your current work session.

API stands for application programming interface. APIs serve as a way for applications to talk to one another, in our case python to some other application like twitter or another data-supplying website. Python can use APIs to pull data automatically from those other applications. Below is an example of how to use an API using some of the code that we used in class, adapted for my own use. My own comments are added to narrate what each part of the code does.

```
#First, we need to import the libraries we will be using. Requests allows us to use our API, while os allows us to read and write to folders on our local files.
import requests
import os

#This is the url we will be using with requests to get to where the data is stored.
url = "https://api.covidtracking.com/v1/states/daily.csv"

#Next, we need to make a place for our data to go. The below lines make the path to where our data will be stored as well as the name of our new CSV.
data_folder = 'C:/Users/Andrew/Desktop/COLLEGE STUFF/Spring 2021/Intro Data Science/' #This line must be edited pending your own file locations
if not os.path.exists(data_folder):
    os.makedirs(data_folder)
# Now we need to make a file name. We are only going to do this once, so the file name can be shortened for our one-time use.
file_name_onetime = 'COVIDdata.csv'
file_name = os.path.join(data_folder, file_name_onetime)

file_name

# Next, we download our data using the requests library. The below command will get the data from the API.
r = requests.get(url)

# Now, we write the data to our local file.
# Using the 'with' statement will immediately close the file once we are done writing
with open(file_name, 'wb') as f:
    f.write(r.content)
    
#Now the data is saved, but we still need to open it in our current work session! This can be done simply with read_csv.
dataset = pd.read_csv(data_folder + '/COVIDdata.csv')
```

## Question 9
##### Describe the apply() function from the pandas library. What is its purpose? Using apply() to various class objects is an alternative (potentially preferable approach) to writing what other type of command? Why do you think apply() could be a preferred approach?

The apply() function in pandas allows you to apply a function to every value of a series. This allows us to quickly create indices or assign new values to to a series with a higher level of control, as you are the one making the function. Using apply() can be a strong alternative to looping over a data frame with indices. Using apply() will likely be faster than a loop, which for large sets of data can make a huge difference in the time it takes for your code to run. 

## Question 10
##### Also describe an alternative approach to filtering the number of columns in a data frame. Instead of using .iloc, what other approach might be used to select, filter and assign a subset number of variables to a new data frame?

