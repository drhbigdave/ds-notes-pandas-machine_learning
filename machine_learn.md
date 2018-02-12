

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

### Following udemy steps:
- relevant notebooks:
Logistic Regression Project Study material - null accuracy.ipynb

Notebook found here, with great details:
http://www.ritchieng.com/machine-learning-evaluate-classification-model/

#### A little EDA

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
- various means of investigating correlations
```
x = ad_data['Age']
y = ad_data['Daily Time Spent on Site'] #udemy class looking at what correlates with time on site - only 1 feature here
sns.jointplot(x=x, y=y, data=ad_data, kind="kde") #shows how the 2 columns data correlates
```
- pair plots for the whole df is a nice one stop shop for initial evaluation
```
sns.pairplot(ad_data)
```

#### Actual regression: train_test_split, fit, predict
First thing we need to do is split our data into an x array with the features to train on and a y array containing the target variable
note: can throw out text/string data as without running NLP linear regression cannot use non-numerical data, obvi you'd keep it if you were going to apply NLP to it.

a good note on linear vs logistical:
https://stackoverflow.com/questions/12146914/what-is-the-difference-between-linear-regression-and-logistic-regression

- import stuff
```
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression #when the outcome is categorical
from sklearn.linear_model import LinearRegression #when the outcome is continuous
from sklearn.linear_model import Lasso #reduces the weight of less useful features
from sklearn.linear_model import Ridge #increases the penalty for less useful features

from sklearn.cross_validation import train_test_split
```

- split your data
```
ad_data.columns #couple of steps to determine features/columns
ad_data['Ad Topic Line'].nunique() #in the exercise the we looked at the cols, chose those to keep and those to be rid of \
here 'Ad Topic Line' had 1000 unique entries (the same # as rows in df) rendering it not useful
X = ad_data[['Daily Time Spent on Site', 'Age', 'Area Income','Daily Internet Usage', 'Male', ]] #the chosen features
y = ad_data['Clicked on Ad' #the predicted class
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, random_state=101) #split it up
```

- train and fit your data
```
log_reg = LogisticalRegresssion() #instantiate your model, in this case a logistical regression model
log_reg.fit(X_train, y_train)
log_reg.coef_ #shows a coef value for each feature, indicating the strength and direction of the correlation
```


#### Evaluate

- import stuff
```
from sklearn.metrics import classification_report
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score
```

- create your predictions variable
```
predictions = log_reg.predict(X_test)
```

- print the evaluations:
```
print(classification_report(y_test, predictions)) #evaluates known test values against the models predictions
print('\n')
print(confusion_matrix(y_test, predictions)) #evaluates known test values against the models predictions
print('\n')
print(accuracy_score(y_test, predictions)) 
```

#### Compare model's accuracy to null value, the result you'd get just choosing the most frequently found category value

taken from this good study source:
http://www.ritchieng.com/machine-learning-evaluate-classification-model/

```
y_test.value_counts() # examine the class distribution of the testing set (using a Pandas Series method)

# calculate the percentage of ones
# because y_test only contains ones and zeros, we can simply calculate the mean = percentage of ones
y_test.mean()

# calculate the percentage of zeros
1 - y_test.mean()

# calculate null accuracy in a single line of code
# only for binary classification problems coded as 0/1
max(y_test.mean(), 1 - y_test.mean())
```

Conclusion:

Classification accuracy is the easiest classification metric to understand
- But, it does not tell you the underlying distribution of response values -- We examine by calculating the null accuracy
- And, it does not tell you what "types" of errors your classifier is making


# Evaluate accuracy of model on test set
print("Accuracy: %0.3f" % dt.score(X_test, y_test))

# Evaluate ROC AUC score of model on test set
print('ROC AUC: %0.3f' % roc_auc_score(y_test, dt.predict_proba(X_test)[:,1]))










