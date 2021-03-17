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

```
Training: 0.021
Testing: -0.002
```
These are very weak R^2 values, meaning that the model does not do very well at predicting the price of a house based on the beds, bath, and square footage data it was given. Because the outputs were so weak, we can do a few things like standardizing our features or using a different model to try and find a better predictor.


## Question 2
##### Now standardize your features (again beds, baths and area) prior to training and testing with a linear regression model (also again with asking price as your target). Now how did your model perform? What were the training and testing scores you produced? How many folds did you assign when partitioning your training and testing data? Interpret and assess your output.

This question is very similar to the last one, with the exception of standardizing our data to try and make the model fit our data more strongly. The idea behind scaling data is that variables going in to models often use different scales. Scaling data puts all of your data on the same scale, commonly with a mean of 0 and a standard deviation of 1. By doing this, the data is transformed and it can be easier for the model to fit it. In our work, an example would be how the scale of how many beds are in a house is completely different from how much square footage there is in a house. By standardizing the data, these data points will be more similar and we could tehreby find a better fitting model. 

We can alter our previously used code to run the same model, but this time with standardized data. The major alterations to the below code from the code from the above question is the addition of using ss (SimpleScaling) on the original dataset 'homes'. The new dataset 'homes_tform' is then input to the same model. I did not change the number of folds from 7, as I found it consistently better R^2 outputs than other fold numbers that I tried.

```
homes_tform = ss.fit_transform(homes)
homes_tform.shape

Xt = homes_tform[:,1:3]
yt = homes_tform[:,0]

kf = KFold(n_splits = 7, shuffle = True)
train_scores = []
test_scores = []

for idxTrain,idxTest in kf.split(Xt):
    Xtrain = Xt[idxTrain, :]
    Xtest = Xt[idxTest, :]
    ytrain = yt[idxTrain]
    ytest = yt[idxTest]
    lin_reg.fit(Xtrain, ytrain)
    train_scores.append(lin_reg.score(Xtrain, ytrain))
    test_scores.append(lin_reg.score(Xtest, ytest))

print('Training after standardization: ' + format(np.mean(train_scores), '.3f'))
print('Testing after standardization: ' + format(np.mean(test_scores), '.3f'))
```

Running the above code gave the following output:

```
Training after standardization: 0.019
Testing after standardization: 0.010
```

Our model improved! While the training R^2 value is marginally lower than it was when our data was not standardized, our testing R^2 value rose realatively more and is now out of the negatives. This means we are on the right track, but these scores are still very low and we can continue trying things to try to improve the model.


## Question 3
##### Then train your dataset with the asking price as your target using a ridge regression model. Now how did your model perform? What were the training and testing scores you produced? Did you standardize the data? Interpret and assess your output.

As mentioned earlier, some ways that we can try to improve our modeling are to standardize the data or to try a different model. We tried standardizing the data and got a minimal improvement, so now we can try a different model on the same data and see if that improves our R^2 values at all. For this question, we will use ridge regression. Ridge regression is a type of modeling that regularizes the factors in a model, essentially adding bias the model in order to punish factors that have too big an effect on the model. Results on the testing data may be a little worse, but in the long run the model can fit the data better with ridge regression as it combats overfitting.

Using a ridge regression will take different code than a KFold, though KFold is still involved in the process. The following code will not only give us the R^2 scores for our training and testing data, but also the optimal alpha value for the model. Alpha is a hyperparameter that determines how much the features of a model are punished for overfitting. The code to get this information is below.

```
# Defining DoKFold
def DoKFold(model, X, y, k, standardize=False):
    from sklearn.model_selection import KFold
    if standardize:
        from sklearn.preprocessing import StandardScaler as SS
        ss = SS()

    kf = KFold(n_splits=k, shuffle=True)

    train_scores = []
    test_scores = []

    for idxTrain, idxTest in kf.split(X):
        Xtrain = X[idxTrain, :]
        Xtest = X[idxTest, :]
        ytrain = y[idxTrain]
        ytest = y[idxTest]

        if standardize:
            Xtrain = ss.fit_transform(Xtrain)
            Xtest = ss.transform(Xtest)

        model.fit(Xtrain, ytrain)

        train_scores.append(model.score(Xtrain, ytrain))
        test_scores.append(model.score(Xtest, ytest))

    return train_scores, test_scores

train_scores, test_scores = DoKFold(lin_reg,X,y,10)
print('Training: ' + format(np.mean(train_scores), '.3f'))
print('Testing: ' + format(np.mean(test_scores), '.3f'))

#Starting the Ridge Regression
from sklearn.linear_model import Ridge

a_range = np.linspace(0, 100, 100)
# a_range = np.linspace(5, 15, 100)
# a_range = np.linspace(7, 8, 100)

k = 7

avg_tr_score=[]
avg_te_score=[]

for a in a_range:
    rid_reg = Ridge(alpha=a)
    train_scores,test_scores = DoKFold(rid_reg,X,y,k,standardize=False)
    #train_scores,test_scores = DoKFold(rid_reg,X,y,k,standardize=True) #To standardize, use this line instead
    avg_tr_score.append(np.mean(train_scores))
    avg_te_score.append(np.mean(test_scores))

idx = np.argmax(avg_te_score)
print('Optimal alpha value: ' + format(a_range[idx], '.3f'))
print('Training score for this value: ' + format(avg_tr_score[idx],'.3f'))
print('Testing score for this value: ' + format(avg_te_score[idx], '.3f'))
```

With 7 folds and unstandardized data, we get the following output:

```
Optimal alpha value: 28.283
Training score for this value: 0.019
Testing score for this value: 0.014
```

If we again use 7 folds but standardize the data by inputting "standardize=True" in to our DoKFold function, we get this output instead:

```
Optimal alpha value: 94.949
Training score for this value: 0.020
Testing score for this value: 0.016
```

Standardizing the data seemed to help in this case! The scores still aren't great, but they are our best yet in both training and testing scores. The standardization seemed to again help the testing scores for the most part.

## Question 4
##### Next, go back, train and test each of the three previous model types/specifications, but this time use the dataset charleston_act.csv (actual sale prices). How did each of these three models perform after using the dataset that replaced asking price with the actual sale price? What were the training and testing scores you produced? Interpret and assess your output.

Now we get to use a new set of data! This dataset has similar features as the original dataset, but the prices now are the prices houses actually sold for instead of the prices that sellers are asking for. I believe the data may fit into a linear model better in this case, as in buying a house there is often some level of negotiation that could bring prices closer to a realistic proportion to the houses' amenities. We will be using the exact same code and situations as before, but now with our new dataset. Below I include the code to input this new dataset (and the optimal number of folds used), as well as the outputs of each of our code blocks above. I do not include the code again as it is very similar or exactly the same as the code used before.

Inputting the new dataset and seeing its shape:
```
homes = pd.read_csv('C:/Users/Andrew/Desktop/COLLEGE STUFF/Spring 2021/Intro Data Science/charleston_act.csv')
homes.shape
```
The shape is (660,28), slightly smaller than our last dataset by about 50 houses. 

KFold without standardization (8 folds):
```
Training: 0.004
Testing: -0.010
```

KFold with standardization (7 folds):
```
Training after standardization: 0.004
Testing after standardization: -0.012
```

Ridge Regression without standardization (5 folds):
```
Training score for this value: 0.004
Testing score for this value: -0.003
```

Ridge Regression with standardization (6 folds):
```
Training score for this value: 0.004
Testing score for this value: -0.002
```

Interestingly enough, each of the models using the actual price of the houses in question performed worse than they did with the asking prices of each of the houses. Of the models with the new data, the ridge regression with standardization performed the best, but the values are astonishingly low. Compared to the models in the last dataset, the outlook is even worse as the earlier models consistently scored 4 times higher than the new ones. This could be explained by the actual price having an opposite effect than I predicted. The data could be harder to model because the asking prices are set under the influence of appraisors (potentially a more structured way of pricing), whereas the actual prices are skewed by people's personal preferences.


## Question 5
##### Go back and also add the variables that indicate the zip code where each individual home is located within Charleston County, South Carolina. Train and test each of the three previous model types/specifications. What was the predictive power of each model? Interpret and assess your output.

To include the zip code variables, we can simply run the same code that we did earlier after re-subsetting our dataset to include the zip code variables. The zip code variables are coded with the column names being the zip code, a 1 being given if the house is in that zip code, and a 0 if the house is not in that zip code. Below is code from earlier now modified to include the 28 columns in our dataset. The code comes directly after reading in the dataset to our IDE.

```
X = np.array(homes.iloc[:,1:28])
y = np.array(homes.iloc[:,0])
```
Below is a table with the Charleston asking prices model outputs:

Analysis Type      |    Number of Folds     | Training R^2  | Testing R^2 | 
|:-------------:|:-------------:|:-----:|:-------------:|
| | KFold without standardization | 9 | 0.282 | 0.214 |
| KFold with standardization | 8 | 0.281 | 0.226 | 
| Ridge Regression without standardization | 10 | 0.261 | 0.219 |
| Ridge Regression with standardization | 8 | 0.279 | 0.272 |


Below is a table with the Charleston actual prices model outputs:

Analysis Type      |    Number of Folds     | Training R^2  | Testing R^2 | 
|:-------------:|:-------------:|:-----:|:-------------:|
| | KFold without standardization | 10 | 0.340 | 0.254 |
| KFold with standardization | 5 | 0.341 | 0.282 | 
| Ridge Regression without standardization | 8 | 0.337 | 0.274 |
| Ridge Regression with standardization | 10 | 0.336 | 0.288 |

The models are way better now! It looks like adding the zipcode data made a huge difference in improving the guessing power of the models in every single model we tested. While the R^2 scores are still not very high, overall adding the zipcode data was a definite net positive, perhaps because the zipcodes allowed for some level of categorization based on neighborhoods. Zipcodes often have similar levels of income and therefore housing prices, so it is not really surprising that the added data was a huge help to our models.

## Question 6
##### 
