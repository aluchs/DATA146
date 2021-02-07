# Project 1.5

This project involves 3 simple questions on manipulating pandas dataframes. Below I have added each question and my solutions to each of them. First, we must import pandas and create a path to our dataset so that it can be imported. 

```
import pandas as pd
path_to_data = 'C:/Users/Andrew/Desktop/COLLEGE STUFF/Spring 2021/Intro Data Science/Week 2/gapminder.tsv'
data = pd.read_csv(path_to_data, sep = '\t') 
data.head()
```

## Exercise 1
### Get a list of all the years in this data, without any duplicates. How many unique values are there, and what are they?

First, we need to get a list of all of the unique instances in the 'years' column of our dataset. This can be done simply with the .unique() function. We then print the function to make sure that there are no duplicates in our new list, and to show what the unique values are.

```
uniqueyears = data.year.unique()
print(uniqueyears)
```

The unique values are [1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 2002 2007]. To answer the next part of the question, we should find out how long our list is. We can do this by using len() to get the answer of 12 unique years.

```
print(len(uniqueyears))
```

## Exercise 2
### What is the largest value for population (pop) in this data? When and where did this occur?

To find the largest population value in our dataset, we can use the .max() function on the 'pop' column of the dataset. The function .max() finds the highest value in a column, which we can assign to an object to figure out when and where the highest population occured.

```
maxpop = data['pop'].max() #Finds the highest value in the 'pop' column and assigns it to an object
print(maxpop) #Prints our new object to make sure the output looks correct
```
Next, we use .loc to find out which row the max population value  of 1,318,683,096 occured. 

```
maxpopcontext = data.loc[data['pop'] == maxpop] #Use .loc to find rows where maxpop was their population value
print(maxpopcontext) #Prints out the results of our last function.
```
Based on the row that we pulled with .loc, we can see that the highest population in the dataset occured in China in 2007.

## Exercise 3
### Extract all the records for Europe. In 1952, which country had the smallest population, and what was the population in 2007?

To answer the first part of this question, we must subset the data to only find rows with 'Europe' in the 'continent' column. After getting that subsetted data, we can subset our new dataset to only include rows that have a 'year' value of 1952. This can be accomplished using the below code.

```
europeonly = data.loc[data['continent'] == 'Europe']
print(europeonly) #Check our output to make sure everything looks correct
europeonly1952 = europeonly.loc[europeonly['year'] == 1952] #subsets our dataset with Europe only to get only rows that have a 'year' value of 1952
print(europeonly1952) #Print our output to make sure our past work looks correct
```
Our next task is to find the smallest population within our new dataset. This can be done using .min(), which does the same thing as .max() but for the smallest value in a list. After finding that value and assigning it to an object, we can use .loc similarly to how we did earlier and find the row that contains the minimum value.

```
minpop = europeonly1952['pop'].min() #Finds the minimum population within our subsetted data of rows including Europe and the year 1952
print(minpop)
minpopcontext = europeonly1952.loc[europeonly1952['pop'] == minpop] #Pulls the row that has our minimum population value out
print(minpopcontext) #Prints our work to see the minimum population value.
```
After running the above code, we find that Iceland had the smallest population in 1952 at 147,962 people. With that information we can go back to our original dataset and subset it to only include rows where the 'country' value is Iceland and the year is 2007.

```
Icelandonly = data.loc[data['country'] == 'Iceland']
Iceland2007 = Icelandonly.loc[Icelandonly['year'] ==  2007]
print(Iceland2007)
```
We can see through the above work that the population of Iceland in 2007 had grown to 301,931 people. Still a small country, but more than doubled its population in the last 50 years!
```
