## eventually move the notes into the relevant topics markdown file

- Feb 8 Class
Scaling

Normailizing is getting all of our values between 0 and 1

Standardization is getting all the values around zero and 

advanced_sklearn.ipynb - GA with scaled data, KNeighborsClassifier,StandardScaler - good classification example

StandardScalar "good for anything with classification"

grid_search.ipynb GA - cross_val_score,GridSearchCV, RandomizedSearchCV - good pipeline

sklearn info:
http://scikit-learn.org/stable/modules/cross_validation.html

- KNN accuracy on original data
```
knn = KNeighborsClassifier(n_neighbors=3)
knn.fit(X_train, y_train)
y_pred_class = knn.predict(X_test)

from sklearn import metrics
print(metrics.accuracy_score(y_test, y_pred_class))
```
- KNN accuracy on scaled data
```
knn.fit(X_train_scaled, y_train)
y_pred_class = knn.predict(X_test_scaled)

print(metrics.accuracy_score(y_test, y_pred_class)) 
```





- feature = synonmous with attribute, property or field;  measurable information about something; a model's inputs
In machine learning and pattern recognition, a feature is an individual measurable property or characteristic of a phenomenon being observed. Choosing informative, discriminating and independent features is a crucial step for effective algorithms in pattern recognition, classification and regression.


- feature engineering - engineering the features themselves to get a good model

- dependent variable - thing you are looking to predict

- ordinal variable - An ordinal variable is a categorical variable for which the possible values are ordered. Ordinal variables can be considered “in between” categorical and quantitative variables.

- regression - In statistical modeling, regression analysis is a statistical process for estimating the relationships among variables. It includes many techniques for modeling and analyzing several variables, when the focus is on the relationship between a dependent variable and one or more independent variables (or 'predictors')

- classification - In machine learning and statistics, classification is the problem of identifying to which of a set of categories (sub-populations) a new observation belongs, on the basis of a training set of data containing observations (or instances) whose category membership is known.


- 2 types of machine learning: supervised, unsupervised

- Supervised learning: labeled data, often historical, used to predict future
- supervised: each observation (row of data) came with one or more labels, either categorical variables (classes) or measurements (regression)


- Unsupervised learning: unlabeled data, look for- extract structure in the data
* example: segment grocery store shoppers into clusters that exhibit similar behaviors
* goal is 'representation'
* Unsupervised learning has a different goal: feature discovery
* Clustering is a common and fundamental example of unsupervised learning
* Clustering algorithms try to find meaningful groups within data
* looking for similar sized clusters
* use clustering on population based data to see if there is a discrete cluster I hadn't seen/known before
* find a cluster, investigate its usefullness as a feature
##### clustering algos (we used)
k-means
dbcluster - density based spatial clustering of applications with noise
*2 parameters: Epsilon and 
Two parameters:
min_samples: specifies how many neighbors a point should have to be included into a cluster.
Epsilon (eps): specifies how close points should be to each other to be considered a part of a cluster; 

Clustering with Scikit-Learn-Solutions.ipynb
Clustering_Drinks_Solution.ipynb

- Reinforcement learning: used for gaming, navigation, robotics, learns by trial and error which actions yield the greatest rewards

#### References and links
http://www.sthda.com/english/wiki/dbscan-density-based-clustering-for-discovering-clusters-in-large-datasets-with-noise-unsupervised-machine-learning

http://www.ritchieng.com/machine-learning-evaluate-classification-model/

https://python-graph-gallery.com/

http://setosa.io/ev/ordinary-least-squares-regression/

http://scikit-learn.org/stable/modules/clustering.html#adjusted-rand-index

https://www.reddit.com/r/learnprogramming/comments/379vwn/visually_learning_algorithms/

http://setosa.io/ev/ordinary-least-squares-regression/
