# Project 3

## Now we're in the weeds - this project involves 4 questions on linear regression and ridge regression combined with more basic python techniques of slicing, loops, and creating functions.

## Question 1
##### Download the dataset charleston_ask.csv and import it into your PyCharm project workspace. Specify and train a model the designates the asking price as your target variable and beds, baths and area (in square feet) as your features. Train and test your target and features using a linear regression model. Describe how your model performed. What were the training and testing scores you produced? How many folds did you assign when partitioning your training and testing data? Interpret and assess your output.

The first step of every analysis, of course, is to load our data into our workspace. This can be done relatively simply as is in the first few lines the code below. Additionally, we will import the functions and libraries that we will be using in our code, like pandas, numpy, and KFold, among others. We then use .shape to get a better sense of what the dataset looks like. Knowing those factors will help us to subset the data so that we are properly inputting our features into the model. In this case, we are inputting the number of beds, bath, and square footage of houses to try and estimate the asking price of the house. We can susbset the inputs for our regression accordingly.

We will be using KFold here for our model, specifically with 7 splits. I input several different fold numbers and eventually found that 6 folds gave me the optimal R^2 in the model. The below code was used to input our dataset into the workspace, import the functions and libraries we will be using, and create our first model.

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import KFold
from sklearn.linear_model import Ridge
from sklearn.preprocessing import StandardScaler

ss = StandardScaler()
lin_reg = LinearRegression()

#Question 1

homes = pd.read_csv('C:/Users/Andrew/Desktop/COLLEGE STUFF/Spring 2021/Intro Data Science/charleston_ask.csv')
#homes = pd.read_csv('C:/Users/Andrew/Desktop/COLLEGE STUFF/Spring 2021/Intro Data Science/charleston_act.csv')
homes.shape


X = np.array(homes.iloc[:,1:4])
#X = np.array(homes.iloc[:,1:28])
y = np.array(homes.iloc[:,0])

kf = KFold(n_splits = 6, shuffle = True)
train_scores = []
test_scores = []

for idxTrain,idxTest in kf.split(X):
    Xtrain = X[idxTrain, :]
    Xtest = X[idxTest, :]
    ytrain = y[idxTrain]
    ytest = y[idxTest]
    lin_reg.fit(Xtrain, ytrain)
    train_scores.append(lin_reg.score(Xtrain, ytrain))
    test_scores.append(lin_reg.score(Xtest, ytest))

print('Training: ' + format(np.mean(train_scores), '.3f'))
print('Testing: ' + format(np.mean(test_scores), '.3f'))
```

Running the above code gives the following output:

Training: 0.021
Testing: -0.002

These are very weak R^2 values, meaning that the model does not do very well at predicting the price of a house based on the beds, bath, and square footage data it was given. Because the outputs were so weak, we can do a few things like standardizing our features or using a different model to try and find a better predictor.


## Question 2
##### Now standardize your features (again beds, baths and area) prior to training and testing with a linear regression model (also again with asking price as your target). Now how did your model perform? What were the training and testing scores you produced? How many folds did you assign when partitioning your training and testing data? Interpret and assess your output.

This question is very similar to the last one, with the exception of standardizing our data to try and make the model fit our data more strongly. The idea behind scaling data is that variables going in to models often use different scales. Scaling data puts all of your data on the same scale, commonly with a mean of 0 and a standard deviation of 1. By doing this, the data is transformed and it can be easier for the model to fit it. In our work, an example would be how the scale of how many beds are in a house is completely different from how much square footage there is in a house. By standardizing the data, these data points will be more similar and we could tehreby find a better fitting model. 
