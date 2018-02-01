##### Fit a DBSCAN estimator
estimator = DBSCAN(eps=.3, min_samples=12)
X = iris[["sepal_length", "petal_length"]]
estimator.fit(X)

##### Clusters are given in the labels_ attribute
labels = estimator.labels_
print (Counter(labels))

colors = set_colors(labels)
plt.scatter(iris['sepal_length'], iris['petal_length'], c=colors)
plt.xlabel("x")
plt.ylabel("y")
plt.show()

##### Fit a k-means estimator
estimator = KMeans(n_clusters=3)
X = iris[["sepal_length", "petal_length"]]
estimator.fit(X)
##### Clusters are given in the labels_ attribute
labels = estimator.labels_
Counter(labels)

##### Plot the data
colors = set_colors(labels)
plt.scatter(iris["sepal_length"], iris["sepal_width"], c=colors)
plt.xlabel("sepal_length")
plt.ylabel("sepal_time")
plt.show()

#### Evaluate
http://scikit-learn.org/stable/modules/clustering.html#silhouette-coefficient
http://scikit-learn.org/stable/modules/clustering.html#adjusted-rand-index