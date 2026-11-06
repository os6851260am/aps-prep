# Machine Learning

> "In **Machine Learning**, we mainly studied how to train computer models to learn from historical data to make predictions.
> 
> 
> The course was divided into two main categories:
> 
> - **Supervised Learning**: where we have labeled data. We covered **Linear Regression** for continuous value prediction, and classification models including **KNN**, **Naive Bayes**, **Support Vector Machines (SVM)**.
> - **Unsupervised Learning**: where data has no labels. We mainly focused on **K-Means Clustering** to find hidden groups."

# Supervised

## Regression

### Linear Regression

"Linear Regression fits a straight line to map input features to a continuous output, formulated as $y = wx + b$. We define a **Mean Squared Error (MSE)** loss function to measure the prediction error, and use **Gradient Descent** to minimize the loss and update the weights." 

## Classification

### KNN

 "KNN is a supervised classification algorithm. The main idea is very intuitive: similar things are close to each other.
When we have a new test point:
1. We calculate the distance between this point and all training points, usually using **Euclidean distance**.
2. We pick the K nearest points.
3. We take a **majority vote**. The most common label becomes the prediction.
For example, if K=3, and we have two circles and one square around the point, we predict it as a circle."

### Naive Bayes

"Naive Bayes is a classification model based on **Bayes' Theorem** and probability.

It calculates the probability of each class for a given input, and chooses the class with the highest probability.

Why is it called 'Naive'? Because it makes a simple assumption: **all features are independent of each other**. In real life, features might be related, but this assumption makes calculation very fast and simple.
A common application is spam email detection."

### Support Vector Machine

"SVM is a powerful model for classification. The goal is to find an optimal line, or a **hyperplane**, to separate two classes.

The margin is the distance between the line and the closest data points. We want to maximize the **margin**.

These closest data points are called **Support Vectors**, because they support and define the margin.

If the data cannot be separated by a straight line, we use the **Kernel Trick**. It projects the data into a higher dimension where a straight line can easily separate them."

# Unsupervised

### K-Means Clustering

"K-Means is an **unsupervised** algorithm. It groups unlabeled data into K clusters.
The steps are very easy:
1. We choose K, and randomly pick K points as center points, called **centroids**.
2. We calculate the distance from every data point to each centroid, and assign each point to its nearest centroid.
3. We calculate the average position of the points in each cluster, and move the centroid there.
4. We repeat step 2 and step 3 until the centroids stop moving."