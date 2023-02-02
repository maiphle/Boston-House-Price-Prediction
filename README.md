# Boston House Price Prediction
A regression model using RapidMiner to predict the price of  houses based on some specific features. 

## Part 1: Data Understanding
### 1.1 Data Description

The dataset includes information on 506 houses in Boston. There are fourteen variables that are all scale variables. Each variable shows the minimum, maximum, mean, and standard deviation. As seen in the table below, the minimum ranges from 0 to 187. The maximum ranges from 0.871 to 396.9. The mean ranges from 0.069 to 408.237. The standard deviation ranges from 0.116 to 168.537. The target (dependent) variable in this dataset is MEDV (Median value of owner-occupied homes in $ 1000's).


### 1.2 Data Visualization

[Images  will be added]

Part 2: Data Preparation
### 2.1 Correlation analysis
 
The feature that was highly correlated with the dependent variable was RM at 0.695. The variables that were moderately correlated with the dependent variable were ZN and B. There were no multicollinearity issues in this comparison between MEDV and all other variables excluding MEDV versus MEDV. Otherwise, there are only two multicollinearity issues detected between two predictor variables which are RAD versus TAX and INDUS versus NOX.


### 2.2 Multicollinearity Issue
The first attributes were RAD and INDUS, and their second attributes were TAX and NOX. The correlation between RAD and TAX was 0.910 and the correlation between INDUS and NOX was 0.764. 
The root mean squared error (RMSE) is the square root of the variance of the residuals. It indicates the absolute fit of the model to the data–how close the observed data points are to the model’s predicted values. Lower values of RMSE indicate better fit. RMSE is a good measure of how accurately the model predicts the response, and it is the most important criterion for fit if the main purpose of the model is prediction. Meanwhile, R-squared (or squared correlation) is a relative measure of fit, higher values indicate better fit, which indicate proportional  improvement in the regression model. Based on this fact, we compared the RMSE and squared correlation outputs of cross validation and split validation datasets to test the performance after excluding each of the variables. We have decided to exclude TAX and INDUS. The output performance values can be seen in the tables below. The RMSE and squared correlation of excluding TAX and INDUS shows a better model fit because the RMSE is lower and the squared correlation is higher in this case. Therefore, we chose to remove TAX and INDUS while keeping RAD and NOX.

### 2.3 Data Normalization
To normalize, first we select all variables, then we select attribute filter type single, then the attribute as MEDV. After that we used invert selection to select all variables except MEDV. We then used the method of range transformation which is the min of 0.0 and the max of 1.0. We need to do normalization in this analysis because normalization is the technique used to organize data in a database. This is important because it minimizes redundancy or duplicate data, and it also makes sure that only relational data is stored in each table. This also can prevent issues like insertions, updates, and deletions that can happen due to database modifications. 

### 2.4 Data Outliers
We used the detect outlier (or distances) operator. We used this function with a number of 10 neighbors and 10 outliers, with a distance function of euclidian distance. After removing the outliers, the root means squared is lower and the squared correlation is higher than keeping the outliers. We removed the outliers from the analysis because they were affecting our assumptions of the data, but not the results of the data. We detected the outliers shown below:

## Part 3: Modeling and Evaluation 
### 3.1 Data Modeling

After preparing the data by removing multicollinearity issues and outliers, we built a model to evaluate the analysis. Since the goal is to predict the median value of owner-occupied homes (MEDV) using scaled independent variables, we used the regression algorithm to find the optimal parameters to create the model. To detect any overfitting issues, the data underwent two validation techniques called split -sample and k-fold cross validation where it gets randomly split into a training and a testing dataset. The split-sample validation split the sample by 80% for training and 20% for testing. Meanwhile, the k-fold cross validation divides the sample into four equal portions (or 4-fold where k = 4) where the data is trained using one portion and tested using remaining portions. In both processes, the model performed linear regression on the training dataset and the regression performance is evaluated against the testing dataset performance using root mean squared error and squared correlation. 

### 3.2 Model Accuracy

[table will be added]

### 3.3 Overfitting Analysis

One indicator to detect underfitting and overfitting issues is the root mean squared error (RMSE). In general, lower RMSE indicates better fit models. Plus, when the RMSE in the training and testing datasets are high, we have an underfitting model. On the other hand, when the RMSE is low on the training dataset and high on the testing dataset, we have an overfitting model. Based on the results generated from split-sample validation, the RMSE for the training dataset is at 4.643 +/- 0.000 while for the testing dataset is at 4.413 +/- 0.000. The cross validation shows the trained RMSE at 4.698 +/- 0.599, while the average test error is at 4.726 +/- 0.000. We can see that the RMSE is lower in the testing dataset in both cases, showing that there is no overfitting issue. There does not seem to be an underfitting issue either as the range of the dependent variable is from 5 to 50 so the RMSE in both datasets are not abnormally high.

## Part 4: Results Discussion

## 4.1 Model Summary Results

Model Summary Table (Model-CV)

### 4.2 Variables Evaluation
Based on the Model Summary Table, we see that all variables are statistically significant, except for AGE (proportion of owner-occupied units built prior to 1940) as it is not significant because the p-value is larger than the significance level of 0.05. Most variables also have a high tolerance level which indicates low multicollinearity, except for LSTAT  (percent lower status of the population) and RM (average number of rooms per dwelling) with medium tolerance level. Meanwhile, the importance of each variable is ranked based on the Absolute Standard Coefficient. Standardized coefficients represent the mean change in the predicted variable (MEDV in this case) given a one standard deviation change in the predictor. According to the second table, LSTATwith Absolute Standard Coefficient at 0.41 is the highest important variable. This indicates that LSTATis a stable predictor of MEDV with good generalizability. LSTAT is followed by DIS (weighted distances to five Boston employment centers), RM, and PTRATIO (pupil teacher ratio by town).
 
### 4.3 Predictive Analysis

