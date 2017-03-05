Decision Tree Regression
================

"We are about to hire a new employee and he has mentioned that he had a salary of of 160k at his previous job. So when we contacted his previous employer to verify that, we just received a Posotion wise average salary details from his previous employer. The employee was at level 6 in his previous employer. To go from level 6 to level 7 it takes around 4 years and the new employee was already at level 6 for two years. So we are predicting salary for a level of 6.5"

``` r
# Importing the dataset
setwd("~/Regression Analysis/Data")

dataset = read.csv('Position_Salaries.csv')
dataset = dataset[2:3]

## We need to use feature scaling for machine learning algorithms those are based on Ecludian distances. Regression algorithms like SVR, Polynomial or Decision Tree does not require feature scaling.
 
# Splitting the dataset into the Training set and Test set
# # install.packages('caTools')
# library(caTools)
# set.seed(123)
# split = sample.split(dataset$Salary, SplitRatio = 2/3)
# training_set = subset(dataset, split == TRUE)
# test_set = subset(dataset, split == FALSE)

# Feature Scaling
# training_set = scale(training_set)
# test_set = scale(test_set)

# Fitting the Regression Model to the dataset

#install.packages('rpart')
library(rpart)

# We are adding an extra optional parameter 'Control' to our code to improve the mpdel's performence
regressor = rpart(formula = Salary ~ .,
                  data = dataset,
                  control = rpart.control(minsplit = 1))

# Predicting result
y_pred = predict(regressor, data.frame(Level = 6.5))

#Visualising the Regression Model results (for higher resolution and smoother curve)
# install.packages('ggplot2')
library(ggplot2)
x_grid = seq(min(dataset$Level), max(dataset$Level), 0.01)
ggplot() +
  geom_point(aes(x = dataset$Level, y = dataset$Salary),
             colour = 'red') +
  geom_line(aes(x = x_grid, y = predict(regressor, newdata = data.frame(Level = x_grid))),
            colour = 'blue') +
  ggtitle('Decision Tree Regression Model') +
  xlab('Level') +
  ylab('Salary')
```

![](Decision_Tree_Regression_files/figure-markdown_github/unnamed-chunk-1-1.png)
