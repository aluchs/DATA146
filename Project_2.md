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



## Question 4
##### Using the seaborn library of functions, produce a box and whiskers plot of population for all countries at the given 5-year intervals. Also apply a logarithmic transformation to this data and produce a second plot. Which of the two resulting box and whiskers plots best communicates the change in population amongst all of these countries from 1952 to 2007?

