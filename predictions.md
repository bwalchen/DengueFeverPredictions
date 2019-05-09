# Predicting Dengue Fever Competition

> **Data Scientists**: Maggie Tsang, Ben Walchenbach

## Structure
* Data Prep and Exploration: [README.md](./README.md)
* Dengue Fever Machine Learning Predictions: [predictions.md](predictions.md)

<br>

## Overview

In this project, we will attempt to predict Dengue fever as outlined in [this competition.](https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread])

The steps we will take in our approach includes:
* Prepare our data by normalizing the features provided in the datasets
* Determine the most relevant features using a learning based features selection
* Experiment with 5 different models
* Assess the accuracy of our models
* And create our final predicted number of total cases using our best model, determined by the calculated accuracy of our models


## Data Prep

We prepared our data by normalizing the features in the dataset. Specifically, we made sure our units were consistent by changing any temperatures from Kelvin to Celcius.

Instead of averaging values to replace any NaN values, we decided to drop those columns in order to not introduce any potential inaccuracies or biases to our data.

Instead of blindly going about creating a model for features_test where the total_cases information was not included, we decided to further split our features_train data, which has the total_cases data, so we can validate how accurate our predictions were. From here, we selected the best features before creating our models.


## Feature Engineering and Selection

As we were required to use a learning-based method for our feature selection, we looking into the potential embedded methods of features selection. After hours of research in understanding the learning-based feature selections from both a conceptual and implimentation perspective, we decided to go with Lasso Regression. 

We implimented a 'getBestALpha' function to determine the best alpha value for our regression which would accurately assign weights to each feature, and drop any irrelevant features.

After narrowing down our best alpha value that produced the great accuracy [according to the R^2 value], we selected our main features to begin modeling.


## Modeling

The models we implimented includes:
* Multivariate Linear Regression
* Ridge Regression
* Lasso Regression
* K Nearest Neighbors
* Decision Tree

**Multivariate** regression allowed us to start with an easier, more familiar approach to our modeling process. By inputting 5, 8, 10, and 12 features respectively, we observed the R^2 value to see which features explain the highest degree of variance in our data.

[**Ridge**](https://www.analyticsvidhya.com/blog/2016/01/complete-tutorial-ridge-lasso-regression-python]) regression advantage is that this modeling method tends to prevent overfitting, while also being a method as a learning-based feature selection.

[**Lasso**](https://www.analyticsvidhya.com/blog/2016/01/complete-tutorial-ridge-lasso-regression-python]) regression tends to be the more popular modeling method, as features with a coefficient of zero can be ignored and therefore, the model can potentially be more scalable.

[**KNN**](https://medium.com/@adi.bronshtein/a-quick-introduction-to-k-nearest-neighbors-algorithm-62214cea29c7) great as it makes no previous assumptions about the data. It is a versatile, simple, and often accurate method as it processes similar features among points closes to it.

[**Decision Tree**](http://www.simafore.com/blog/bid/62333/4-key-advantages-of-using-decision-trees-for-predictive-analytics) algorithm provides a degree of feature selection and nonlinear relationships among features don't affect the results.


## Validation

We performed cross validation and a GridSearch with our results from the modeling section. Though depending on how many folds we ran, there was a wide range of the accuracies of our model, from 3% accuracy to 30% accuracy. Overall, lasso regression had the highest level of consistency and accuracy in predicting the total cases of dengue fever.

We plugged in four of our modeling algorithms in a grid search to determine what values would be the best to increase the accuracy of our models.

Additionally, we computed the [RSS](https://en.wikipedia.org/wiki/Residual_sum_of_squares) values for each prediction of our algorithm. We determined that Lasso regression, with the lowest RSS score, was our most accurate model.

## Visualization

Plotting the RSS values on a bar plot, Lasso Regression and Ridge Regression were the most accurate models since it had the smallest RSS values when compared to tha actual total_cases of our training features.

We compared the accuracy of the predictions by plotting the results from the Lasso Predictions and the Ridge Predictions to the actual total_cases, where the closer the results were to a X=Y linear relationship, the more accurate the predictions were.

For our final visualization, we took the values that were outputted by our GridSearch analysis and redid our Lasso Regression. The results were surprisingly similar as the data plots were almost all overlapping with one another.


## Conclusion

Overall, we selected features and multiple validated modeling methods to determin the accuracy of each model and to see if we could predict the total cases of dengue fever in the tropics.
