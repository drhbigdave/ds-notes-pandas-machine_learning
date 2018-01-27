Udemy:
Supervised learning: labeled data, often historical, used to predict future
Unsupervised learning: unlabeled data, look for structure in the data
Reinforcement learning: used for gaming, navigation, robotics, learns by trial and error which actions yield the greatest rewards

Linear regression is that estimator object, it is the model itself

scikit-learn algorithm cheat sheet
http://scikit-learn.org/stable/tutorial/machine_learning_map/index.html


*REGRESSION*

http://www-bcf.usc.edu/~gareth/ISL/ISLR%20Seventh%20Printing.pdf

Least Mean Squares  - classic linear regression
idea behind supervised data - 
labeled data  - our prediction of the son's height
unlabeled  data  - the father's height

## Following udemy steps:
## A little EDA
* A little UDA
```
df.info()
df.describe() #for numerical columns
sns.pairplot(df) #whole df, histograms and correlation scatterplots for all of df
```

- now you'll want to check out the distribution of your target column, what you are trying to predict:
```
sns.distplot(df['price'])
```
- do a table of the correlations between the columns:
```
df.corr()
```
- then you might want to do a heat map of the correlation of each of the columns:
```
sns.heatmap(df.corr())
# or do
sns.heatmap(df.corr(), annots=True) # this will pass in the corr numbers into the map
```

* Actual regression
First thing we need to do is split our data into an x array with the features to train on and a y array containing the target variable
note: can throw out text/string data as without running NLP linear regression cannot use non-numerical data, obvi you'd keep it if you were going to apply NLP to it.


