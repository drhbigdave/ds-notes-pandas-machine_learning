thank you Sayali Sonawane

https://stackoverflow.com/questions/12146914/what-is-the-difference-between-linear-regression-and-logistic-regression

- Linear regression output as probabilities

It's tempting to use the linear regression output as probabilities but it's a mistake because the output can be negative, and greater than 1 whereas probability can not. As regression might actually produce probabilities that could be less than 0, or even bigger than 1, logistic regression was introduced.

Source: http://gerardnico.com/wiki/data_mining/simple_logistic_regression

enter image description here

#### Outcome

- In linear regression, the outcome (dependent variable) is continuous. It can have any one of an infinite number of possible values.

- In logistic regression, the outcome (dependent variable) has only a limited number of possible values.

#### The dependent variable

- Logistic regression is used when the response variable is categorical in nature. For instance, yes/no, true/false, red/green/blue, 1st/2nd/3rd/4th, etc.

- Linear regression is used when your response variable is continuous. For instance, weight, height, number of hours, etc.

#### Equation

- Linear regression gives an equation which is of the form Y = mX + C, means equation with degree 1.

- However, logistic regression gives an equation which is of the form Y = e^X/1 + e^-X

#### Coefficient interpretation

- In linear regression, the coefficient interpretation of independent variables are quite straightforward (i.e. holding all other variables constant, with a unit increase in this variable, the dependent variable is expected to increase/decrease by xxx).

- However, in logistic regression, depends on the family (binomial, Poisson, etc.) and link (log, logit, inverse-log, etc.) you use, the interpretation is different.

#### Error minimization technique

- Linear regression uses ordinary least squares method to minimise the errors and arrive at a best possible fit, while logistic regression uses maximum likelihood method to arrive at the solution.

- Linear regression is usually solved by minimizing the least squares error of the model to the data, therefore large errors are penalized quadratically.

- Logistic regression is just the opposite. Using the logistic loss function causes large errors to be penalized to an asymptotically constant.

Consider linear regression on categorical {0, 1} outcomes to see why this is a problem. If your model predicts the outcome is 38, when the truth is 1, you've lost nothing. Linear regression would try to reduce that 38, logistic wouldn't (as much)2.



