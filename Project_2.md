# Project 2

## This project involves 4 questions on types of data, correlations, data transformation, and data visualization. 

## Question 1
##### Describe continuous, ordinal and nominal data. Provide examples of each. Describe a model of your own construction that incorporates variables of each type of data. You are perfectly welcome to describe your model using english rather than mathematical notation if you prefer. Include hypothetical variables that represent your features and target.

Below are descriptions of continuous, ordinal, and nominal data, as well as examples for each.

Continuous data is data that can take any value within a range. An example would be measuring people's height. Heights do not come in set intervals, like 5' 4", but instead can be any smaller decimal, for instance a number like 5' 4.125". 

Ordinal data is both named and ordered. An example of ordinal data would be a political scale that goes Extremely Conservative - Moderately Conservative - Moderate - Moderately Liberal - Extremely Liberal. This scale is Ordinal data because the data has names (not numeric values) and has an order (the scale wouldn't make sense if we were to put Extremely Liberal and Extremely Conservative on the same side).

Nominal data is named, but not ordered. An example of nominal data would be a survey question asking what type of urban area respondents live in, with set responses like "suburbs", "cities", and "towns". The possible responses each have names, but their order can be mixed up without affecting the question at all. 

We can use the above examples to create an example model that includes variables from each type of data. Lets say we believe that height, political leaning, and the urban area that people live in can predict how much people like going to movie theaters (our target). We can start creating our model by assigning each of our variables, or features, a variable name. We will use the following classifications:

x = Height

y = Political Leaning

z = Urban Area

a = Liklihood of Enjoying Going to Movie Theaters (this is our target)

For simplicity's sake, lets say that we have found multiple studies that indicate that height, political leaning, and urban area each have an equal effect on the liklihood of someone liking visits to the movie theater. If we know each variable has a direct positive relationship with liklihood of enjoying going to movie theaters, we can then make our model the following: a = x + y + z. But how do we plug our nominal and ordinal data in to get a numeric prediction for how likely movie theater enjoyment is for our respondents? By assigning numeric values to the named variables. For political leaning, we can assign each value 1-5 in order from most to least conservative. For the urban area, we can do the same in assigning 1 to towns, 2 to suburbs, and 3 for cities. By assigning each name to numbers, we can plug in each value to get a return value for our target. This is a relatively simplistic model, but in my mind gets across the point of how features interact to predict the target. The variables may be nonsensical, but they can be replaced with other variable names for the same effect.


## Question 2
##### Comment out the seed from your randomly generated data set of 1000 observations and use the beta distribution to produce a plot that has a mean that approximates the 50th percentile. Also produce both a right skewed and left skewed plot by modifying the alpha and beta parameters from the distribution. Be sure to modify the widths of your columns in order to improve legibility of the bins (intervals). Include the mean and median for all three plots.



## Question 3
##### Using the gapminder data set, produce two overlapping histograms within the same plot describing life expectancy in 1952 and 2007. Plot the overlapping histograms using both the raw data and then after applying a logarithmic transformation (np.log10() is fine). Which of the two resulting plots best communicates the change in life expectancy amongst all of these countries from 1952 to 2007?

The first step of any question using a data set is to import the data. In my case, this can be done with the following code. We will use the alias df for our dataset to make later code simpler to write and easier to understand.

```
df = pd.read_csv('C:/Users/Andrew/Desktop/COLLEGE STUFF/Spring 2021/Intro Data Science/gapminder.tsv',sep='\t')
```

Our next step is to create indexes of rows of data that are from the years in question, 1952 and 2007. This can be done relatively simply, and we can use our indexes to create two new dataframes that only include the rows of data we want to see. This can all be done in the code below, which is annotated to say which part does which action.

```
#Creates indicies for rows that hold data from 1952 or 2007
idx_1952 = df['year'] == 1952
idx_2007 = df['year'] == 2007

# Store the data from 1952 and 2007 as 2 new dataframes
df_1952 = df[idx_1952]
df_2007 = df[idx_2007]
```
Now that we have the data we need, we can create the plots comparing the change in life expectancies amongs all countries in the data set from 1952 to 2007. The below code will create our plot, name its axes, and create a legend in the corner so we know which histogram color is showing which year.

```
# Make the plot!
plt.figure(figsize=(6, 6))
plt.hist(df_1952['lifeExp'], rwidth=0.9, label=1952, alpha=0.5)
plt.hist(df_2007['lifeExp'], rwidth=0.9, label=2007, alpha=0.5)
plt.xlabel('Life Expectancy')
plt.ylabel('Number of countries')
plt.legend(loc = "upper left")
plt.show()
```
Running the above code will give us the following plot as its output.

![image](https://user-images.githubusercontent.com/78165529/109752061-b3bd0500-7bad-11eb-803e-f87976737ff1.png)

This looks pretty good! But maybe we can make it better. What if we try applying a logarithm to the data? This can be done with the following code, only slightly altered from the code to make the plot above.

```
plt.figure(figsize=(6, 6))
plt.hist(np.log10(df_1952['lifeExp']), rwidth=0.9, label=1952, alpha=0.5)
plt.hist(np.log10(df_2007['lifeExp']), rwidth=0.9, label=2007, alpha=0.5)
plt.xlabel('$\log_{10}$ Life Expectancy')
plt.ylabel('Number of countries')
plt.legend(loc = "upper left")
plt.show()
```

Running this code gives this output instead:
![image](https://user-images.githubusercontent.com/78165529/109752230-01d20880-7bae-11eb-8260-3b878be9c163.png)

While interesting, I believe that the first plot (without the logarithm) is a better representation of the data. You can clearly see the trend in the data towards a higher life expectancies in 2007, and that trend is shown without altering the data at all. The lack of alteration will make it easier for audiences to understand while still getting the point of the data across. It's not that the logarithm plot is bad, but we can communicate the same information with the unaltered plot with more simplicity, so it is the plot that best communicates the information.


## Question 4
##### Using the seaborn library of functions, produce a box and whiskers plot of population for all countries at the given 5-year intervals. Also apply a logarithmic transformation to this data and produce a second plot. Which of the two resulting box and whiskers plots best communicates the change in population amongst all of these countries from 1952 to 2007?

Creating these plots is similar to the process of creating the plots in Question 3, but this time we do not need to create indicies and new dataframes as we can simply subset the data within the original dataframe. To create our first box and whisker plot, we can use seaborn's boxplot function in the following code.

```
plt.figure(figsize=(8, 8))
sns.boxplot(x=df['year'], y=df['pop'], color='pink')
plt.ylabel('Population in Billions')
plt.xlabel('Year')
plt.show()
```

This code outputs the box and whisker plot below. While it includes all of the information we asked it to include, the data is very difficult to read because of the few outliers that stretch the graph upwards and shrink the boxes that we would like to see. 
![image](https://user-images.githubusercontent.com/78165529/109754648-698a5280-7bb2-11eb-9ca5-231f1dcb4bf9.png)

To try to create a plot that we can discern more information from, we can apply a logarithm to the data using the following code.

```
plt.figure(figsize=(8, 8))
sns.boxplot(x=df['year'], y=np.log10(df['pop']))
plt.ylabel('$\log_{10}$ Population')
plt.xlabel('Year')
plt.show()
```

This code outputs the plot below. While the plot uses a logarithm on the y axis now (which may be conusing to some readers), the trend in the data is more more clearly shown than it was in the previous plot. The extreme outliers have come closer to the main bodies of the box and whisker plots, and it is not much easier to tell that population sizes have been on an upward trend from 1952 - 2007. Because we can much more easily see the trend in the data, this plot clearly communicates the change in population sizes best.

![image](https://user-images.githubusercontent.com/78165529/109754814-b8d08300-7bb2-11eb-9136-fd58134375c3.png)

