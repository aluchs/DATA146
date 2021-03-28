# Midterm

## After a tough midterm, I was knocked down but not out. Below are my second attempts at the midterm questions, and what I did wrong on my first go-through.

## Question 15
##### Which of the below features is most strongly correlated with the target?

I got this question correct on the midterm and feel comfortable with both the concepts and data involved. Most of my past research work has been with similar correlations, so this was a relatively simple question.

## Question 16
##### If the features are standardized, the correlations from the previous question do not change.

This question was also relatively simple, as standardizing helps to put the measures involved in a dataset on to the same scale, but does not change the measures relative to one another. Therefore, the correlations are unchanged.

## Question 17
##### If we were to perform a linear regression using only the feature identified in question 15, what would be the coefficient of determination? Enter your answer to two decimal places, for example: 0.12

A silly (and rather unfortunate) mistake was made here. In my original solving of the problem I seem to have forgotten to reshape the data to work in a Linear Regression. While I used the correction function and subsets of the data, I obviously got the answer wrong and can only see that as the difference between my original code and the code that gets the correct answer. That code is below:

```
from sklearn.linear_model import LinearRegression as LR
lin_reg = LR()
np.round(lin_reg.score(X_df['MedInc'].values.reshape(-1,1),y),2)
```

This code snippet first imports the LinearRegression function that we will use to get the correct answer. The next line shows how to get the correlation coefficient between the MedInc data and the targets while simultaneously using np.round to round the answer down to two decimal places, as the question asks. While this is relatively simple code, understanding all parts of the function is important and I have nailed this one into my head.

## Question 18
##### 
