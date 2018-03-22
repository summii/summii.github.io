---
layout: post
title: "Clustering - A Gentle Introduction"
date: 2018-03-18
---

## Clustering

It is a part of unsupervised machine learning models that attempt to group data points into clusters.

**Cluster** - A group of data points that behave similarly.

**Centroid** - Center of a cluster or average point in a cluster.

The purpose of cluster analysis is to enhance our understanding  of a dataset by dividing the data into groups.
The goal is see the hidden structure of data.

In this blog, we will be exploring **k-means** clustering, which is one of the most popular clustering algorithms.

**k** stands here for "partitions of dataset into k clusters"

Let's jump into problem, do you know different types of beer? Here, we will categorize beers based on different quantitative features.

~~~ python

df = pd.read_csv('https://gist.githubusercontent.com/summii/58f7b645bc6d1ac2f002e562264e47a4/raw/bd81c819d0689889223d19d764a5323392e33c22/beers.txt', sep=',')

df.shape

df.head()

~~~

![alt text](/img/cluster1.png)

Here we have 2 beers rows with 5 columns: name, calories, sodium, alcohol, and cost. We like quantitative features, so we will 
ignore names of beer in clustering.

```python
X = df.drop('name', axis=1)
```

Now we will perform K-Means using scikit-learn:


```python
# K-means with 3 clusters
from sklearn.cluster import KMeans
km = KMeans(n_clusters=3, random_state=1)
km.fit(X)
```

K-Means algorithm has come up with three clusters.

```python
# save the cluster labels and sort by cluster
df['cluster'] = km.labels_
```

We can use **groupby** and **mean** to see each cluster

```python
df.groupby('cluster').mean(
```

![alt text](/img/cluster2.png)

We can see that cluster 0 has higher content for every features, these might be good beers and cost more.Cluster 2 has very low content for alcohol and calories, these might be light beers and cost less.

Let's use **pyplot** to make graph:

```python
import matplotlib.pyplot as plt
%matplotlib inline


# save the DataFrame of cluster centers
centers = df.groupby('cluster').mean()
# create a "colors" array for plotting
colors = np.array(['red', 'green', 'blue', 'yellow'])
# scatter plot of calories versus alcohol, colored by cluster (0=red, 1=green, 2=blue)
plt.scatter(df.calories, df.alcohol, c=colors[list(df.cluster)], s=50)

# cluster centers, marked by "+"
plt.scatter(centers.calories, centers.alcohol, linewidths=3, marker='+', s=300, c='black')

# add labels
plt.xlabel('calories')
plt.ylabel('alcohol')
```

![alt text](/img/cluster3.png)




