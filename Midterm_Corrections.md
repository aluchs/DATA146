# Midterm Corrections

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
##### Let's take a look at how a few different regression methods perform on this data.
##### Start with a linear regression.
##### Standardize the data
##### Perform a K-fold validation using:
##### k=20, shuffle=True, random_state=146
##### What is the mean R2 value on the test folds?  Enter your answer to 5 decimal places, for example: 0.12345

Again, silly mistakes. Typos truly are the bane of my existence. In this question I made the unfortunate error of using the wrong dataset in my K-fold validation. For whatever reason I seem to have used a subset dataset I created for the above questions, which of course completely neglects a significant part of the dataset. For the correct answer, one can use the below code to utilize the DoKFold function we created earlier.

```
k=20
train_scores,test_scores,train_mse,test_mse = DoKFold(LR(),X,y,k,True)

print(np.mean(train_scores), np.mean(test_scores))
```

This code snippet simply sets the number of folds we want (20 in this case), then plugs that in to the function we created to print out the mean R^2 value of our test folds. After using this code we get the correct answers of 0.60519 for the training data and 0.62439 for the testing data.

## Question 19
##### (Using ridge regression and the same K-Fold settings as the previous question) For the optimal value of alpha in this range, what is the mean R2 value on the test folds?  Enter your answer to 5 decimal places, for example: 0.12345

For this question, I was conceptually misunderstanding what the code was trying to do. I initially thought that a Ridge regression could be performed, and would then give you the R^2 value of the folds as well as the hyperparameter alpha. In reviewing my notes and discussion in class, I found that instead we are trying to find the alpha value within the range that will give us the best fit in our model. We do this by iterating through the possible alpha values in our range and plugging them in to the model to find the alpha that gives us the highest possible mean R^2. This process can be done with the following code. What the snippet does is uses the DoKFold function we created earlier with a Ridge regression to find the best fit for the model. It uses a process like what is outlined above, and then graphs the average R^2 values as well as their corresponding alpha values (within the range we specificed).

```
from sklearn.linear_model import Ridge, Lasso

rid_a_range = np.linspace(20,30,101)

rid_tr=[]
rid_te=[]
rid_tr_mse=[]
rid_te_mse=[]

for a in rid_a_range:
    mdl = Ridge(alpha=a)
    train, test, train_mse, test_mse = DoKFold(mdl, X, y, k, True)

    rid_tr.append(np.mean(train))
    rid_te.append(np.mean(test))
    rid_tr_mse.append(np.mean(train_mse))
    rid_te_mse.append(np.mean(test_mse))

idx = np.argmax(rid_te)
print(rid_a_range[idx], rid_tr[idx], rid_te[idx], rid_tr_mse[idx], rid_te_mse[idx])
plt.plot(rid_a_range, rid_te,'or')
plt.xlabel('$\\alpha$')
plt.ylabel('Avg $R^2$')
plt.show()
```

Running the following code will give us the optimal alpha value of the range as well as the mean R^2 value of the test folds when using that alpha value. The correct answer is an alpha value of 25.8, which gives us a mean R^2 on the training data of 0.60627 and of 0.60201 on the testing data.

## Question 20
##### Next, try Lasso regression.  Look at 101 equally spaced values between 0.001 and 0.003.
##### Use the same settings for K-fold validation as in the previous 2 questions.
##### For the optimal value of alpha in this range, what is the mean R2 value on the test folds? Enter you answer to 5 decimal places, for example: 0.12345

Same problem, similar code, similar solution. The problems that I had on the last question were the same for this question, which can use the exact same code with different linspace values and Lasso regression instead of Ridge regression. I won't show the code here again for redundancy's sake, but the only things that need to be altered for this question are the linspace bounds, the names in the loop (adapted to reflect that they are showing what happens with a Lasso regression), and the parameters put in DoKFold (adjusted to put in the a Lasso regression this time). Making all of those adjustments gives an optimal alpha value of 0.00186, a mean R^2 of 0.60615 on the training data, and a mean R^2 of 0.60213 on the testing data.

## Question 21
##### Let's look at some of what these models are estimating. 
##### Refit a linear, Ridge, and Lasso regression to the entire (standardized) dataset.  No need to do any train/test splits or K-fold validation here. Use the optimal alpha values you found previously.
##### Which of these models estimates the smallest coefficient for the variable that is least correlated (in terms of absolute value of the correlation coefficient) with the target?

This problem was difficult because of my lack of understanding the previous two questions. Without the proper alpha values, it is not possible to get the correct answer for this question because running the regressions properly requires those alpha values. Besides that issue, my original code seemed relatively correct so I understood the question itself, just not the entire implementation of it. The code snippet that most efficiently solves this problem is as follows:

```
print(X_names[5])
lin = LR(); rid=Ridge(alpha=25.8); las = Lasso(alpha=0.00186)
lin.fit(Xs,y); rid.fit(Xs,y); las.fit(Xs,y);
lin.coef_[5], rid.coef_[5], las.coef_[5]
```

The above snippet firstly prints the column that we will be looking at for this question. It prints 'AveOccup', so now we have a better idea of what exactly we are looking at. The next line defines the settings we will use for the regressions by putting in the alpha values for the question. The third line fits each of the models, and the final line prints out the correlations for each of those models so that we can see which estimates the smallest coefficient for the variable that is least correlated with the target in terms of the absolute value of the correlation coefficient. The final line prints out (-0.03932626697814873, -0.039412573728940394, -0.03761823364553456), which tells us that the Lasso regression gives the smallest correlation coefficient for the variable. 

## Question 22
##### Which of the above models estimates the smallest coefficient for the variable that is most correlated (in terms of the absolute value of the correlation coefficient) with the target?

This question requires similar code to the last one, this time customized to slice out the variable that was most correlated with the target. Because we already input the settings for each of our regressions, the code for this problem takes only two lines:

```
print(X_names[0])
lin.coef_[0], rid.coef_[0], las.coef_[0]
```

The first line prints out the variables name that we are looking at to check that we have the right subset. It prints out 'MedInc' (the median income), so we have the correct index. The next line simply uses the lin, rid, and las settings we used in our last question to find the coefficients for this variable. The second line outputs (0.8296193042804514, 0.8288892465528185, 0.8200140807502059), which tells us that the Lasso regression estimates the smallest coefficient for MedInc, the variable most correlated with the target.

## Question 23
##### If we had looked at MSE instead of R2 when doing our Ridge regression (question 19), would we have determined the same optimal value for alpha, or something different?

