# Project 5 Part 1

## In this episode of DATA146, we take on linear, ridge, and lasso regression, all with minimal assistance. Truly a challenge for the ages, so lets get right into it!

## Question 1
##### Download the anonymized dataset describing persons.csv from a West African county and import it into your PyCharm project workspace (right click and download from the above link or you can also find the data pinned to the slack channel). First set the variable wealthC as your target. It is not necessary to set a seed.

Simple! We can use panda's read_csv to import our .csv file. In looking at the data, there needs to be some cleaning performed as several NaN entries exist in the dataset, which won't work well with our models. We can use dropna to remove these variables. By using .shape, we know that dropping the NaN values brought our dataset from 47,974 entries to 47,891 entries. That means we only lost about 80 rows, which in a dataset of over 47,000 is a minimal loss. Next, we must remove our target variables from the dataset so they do not influence our projections of the model's fit on the data. Specifically, we can use .drop to remove both the wealthC and wealthI variables. 


##Question 2
##### Perform a linear regression and compute the MSE. Standardize the features and again compute the MSE. Compare the coefficients from each of the two models and describe how they have changed.

For this problem we will use LinearRegression from the sklearn library. Now that our dataset is properly cleaned, we can use LinearRegression to calculate the MSE for both WealthI and WealthC as they are and after being standardized. MSE can be calculated with the below line of code once you have your actual y and predicted y from the linear regression.

```
mse = np.mean((y-y_pred)**2)
```

Below is a table showing the MSEs for WealthC and WealthI, both as-is and after being standardized. I used StandardScaler from the sklearn library in otder to standardize the variables. 

| MSEs  | Un-Standardized | Standardized  |
| ------------- | ------------- | ------------- |
| WealthC | 8308093399.704249  | 0.44285065024071685 |
| WealthI  | 1750276834.930475  | 10058370204.424  |

Because MSE is relative, we are not looking to find the objectively best fitting model, but can use our results to compare betweent the models. The standardized WealthC model seemed to do the best by far, to the point where I am wondering if there is an error but could not find any. Regardless, the next best performing model was the WealthI standardized, so across the board standardization seemed to help with our performance. Not too far behind that was the WealthI un-standardized model, and way behind that was the WealthC un-standardized model. 


##Question 3
##### Run a ridge regression and report your best results.

First, we'll run a ridge regression with WealthC as our target variable. The first step in running a ridge regression is to find our alpha parameter. Similar to the midterm, this can be done by using our DoKFold function in a loop for all alpha values in a range. To save time, we will start with a wide range of alpha values but only test ~20 points within that wide range. By doing that, we can quickly scope in to where we believe the best alpha value is located. We'll start by running our ridge regression for 20 values between 50 and 200. The output gives us the below plot.

myplot.png

