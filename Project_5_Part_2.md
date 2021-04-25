# Project 5 Part 2

## Shiny new kinds of models! In this project we take a look at K-nearest neighbors, logistic regression, and random forests using a dataset on a large West African city.

As usual, our first step is to download and import our dataset, as well as create our DoKFold, GetData, and CompareClasses commands. Each of these functions have been used in class before, so it is relatively simple to bring them in to my project. Our dataset requires a bit of preparation, namely dropping NaN values as well as changing the age and edu column types to integers. 

#### Execute a K-nearest neighbors classification method on the data. What model specification returned the most accurate results? Did adding a distance weight help?

I began the project by execurint a K nearest neighbors classification method with a range of 30 to 200. A model specification of 72 returned the most accurate results, specifically with a training score of 0.5639 and a testing score of 0.54482. This result can be seen in the below plot, which visualizes our search for the best possible model specification.

![image](https://user-images.githubusercontent.com/78165529/115970698-25f8f880-a512-11eb-9b59-b1435e42505e.png)

Adding distance as a weight seemed to help the model in the training scores, but did not help in the testing scores. When running the KNN classification method with a range of 10 to 100, I found that a specification of 88 returned the most accurate results, with a training score of 0.7577 and a testing score of 0.4958. The below plot was returned when I was finding the best possible model specification.

![image](https://user-images.githubusercontent.com/78165529/115970614-850a3d80-a511-11eb-9192-049535b0eb29.png)


#### Execute a logistic regression method on the data. How did this model fair in terms of accuracy compared to K-nearest neighbors?

A logistic regression performed on the data compared relatively evenly with the K-nearest neighbors classification methods. The logistic regression returned a training score of 0.5507 and a testing score of 0.5508. Both scores are relatively similar to those from the initial KNN method, and when the distance weight is added the scores are worse in the trianing data but much stronger in the testing data.


#### Next execute a random forest model and produce the results. See the number of estimators (trees) to 100, 500, 1000 and 5000 and determine which specification is most likely to return the best model. Also test the minimum number of samples required to split an internal node with a range of values. Also produce results for your four different estimator values by both comparing both standardized and non-standardized (raw) results.

Out of the four options for number of estimators, 5000 returned the best results, specifically training and testing scores of 0.8004 and 0.5031, respectively. Using a loop, I found that the minumum number of samples required to split an internal node with a range of values was 15, as it gave the best results for for the classification when min_samples_split is between 15 and 30. 

Below is a chart with the model results for our random forest model when the data is both scaled and unscaled.

| Number of Trees     | Scaled | Un-Scaled |
| :---: |    :----:   | :---: |
| 100   | 0.50073     | 0.50610  |
| 500   | 0.50024     | 0.50951     |
| 1000  | 0.50317     | 0.50561     |
| 5000  | 0.49780     | 0.50902     |

As you can see, the models performed relatively similarly, with the un-scaled models doing slightly better. The difference is small, with most results only differing by a few hundredths. Overall, the 500 trees unscaled model seemed to perform the strongest, with the scaled 5000 tree model performing the worst.


#### Repeat the previous steps after recoding the wealth classes 2 and 3 into a single outcome. Do any of your models improve? Are you able to explain why your results have changed?

##### kNN, Weighted and Unweighted
The first step in this process was to combine the the two classes in to one. I elected to make all '2' values in the dataset '3's instead. There were few '2's in the first place and the wealth values go from 2 to 5, so I thought it would make the most sense to alter the data in that way. I then began the process of running the same models to see how combining wealth values affected the model strengths. I began with the unweighted kNN analysis. Using the below plot and a range of 30 to 200, I found that a model specification of 91 would yield the best results. The model performed relatively well, with a .5621 on the training data and a .5436 on the testing data.

![image](https://user-images.githubusercontent.com/78165529/116001623-56e53600-a5c3-11eb-9bb0-fcf71404fa22.png)

I then ran a kNN analysis that included weighting for distance. This go-around I decided to test model specifications between 30 and 200 to make sure that I was finding the best possible specification for the model. I found that a specification of 83 returned the best results, specifically a 0.7582 on the training data and a 0.4961 on the testing data. The below plot shows how the weighting changed the model's strength.

![image](https://user-images.githubusercontent.com/78165529/116001810-7af54700-a5c4-11eb-88e6-69026cfc9658.png)

##### Logistic Regression

The next step was to run a logistic regression. This was relatively simple to run, and I found that the regression returned training and testing scores of 0.5506 and 0.5502, respectively. 

##### Random Forest Model

For my random forest model, I again used the number of estimators as 100, 500, 1000 and 5000. Of the four, 5000 estimators is likely to perform the best, with a score of 0.4924 on the testing data. While stronger than the other estimator values, the difference was minimal. 100 estimators returned a score of 0.4899, so even between the biggest difference in estimator counts, the difference in scores was only about 0.002. 

I also found that the minimum number of samples that returned the best score was 25. Next, I had to run the tree models to see which will actually perform the best. The below table contains my results using both scaled and unscaled data.

| Number of Trees     | Scaled | Un-Scaled |
| :---: |    :----:   | :---: |
| 100   | 0.47877     | 0.49682  |
| 500   | 0.47535     | 0.50268     |
| 1000  | 0.47632     | 0.50610     |
| 5000  | 0.48072     | 0.50707    |

Standardizing the data did the model no favors. As you can see in the table, scores across the board were lower as a result of scaling the data, with the best result being 0.48072 after using 5000 estimators. The lowest unscaled score was 0.49682 so clearly the data should be kept unscaled to make the model as strong as possible.

#### Which was best?

The question of the hour. We've used a bunch of models, but which is actually the best at predicting wealth based on our dataset? The answer is the unweighted k-nearest neighbors classification we performed on the dataset before wealth values 2 and 3 were combined. We recieved scores of 0.5639 on the training data and 0.54482 on the testing data, both relatively solid scores that outperformed most of the random forest models by about .05, a relatively sizeable margin. 
