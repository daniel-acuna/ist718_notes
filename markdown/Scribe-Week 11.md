
# Scribes for Week 11(Apr 9,10)

# Authors: Srinath Ramachandran & Satyen Amonkar

## Problem with Logistic Regression

- One of the problems with Logistic Regression is: When a set of data points belonging to a particular class is surrounded by data points of other classes, then in reality the boundaries between these classes are actually non-linear. However logistic  regression finds a linear relationship between those classes. Hence, Logistic Regression fails to identify boundaries between classes in such scenarios.<br/>


<p align="center">
<img src="https://github.com/srinath31/ist718_notes/blob/master/markdown/image/LogisticProblem.png" width=70%>
</p>

## Remedy to solve the Logistic Regression Problem 

- Remedy for this is through Transformation. For this, we have to center the data and then compute a new feature called distance(from center). This would result in a linear separation and now we can find the boundaries.

<p align="center">
<img src="https://github.com/srinath31/ist718_notes/blob/master/markdown/image/LogisticRemedy.png" width=70%>
</p>

## The XOR Problem


- The problem with this function is that there is no linear function that can correctly classify the data. It is non-separable. 

- The solution for this is Decision Trees.

## Decision Trees

- These are non-linear functions that can be used for both classification and regression problems. Here, we recursively  partition  the space, create regions for the space and assign decisions to each of the regions. 

- The decision of partitioning is done by minimizing the loss functions i.e. those trees are chosen which result in minimum loss.

- Below is an example of a decision tree:

<p align="center">
<img src="https://github.com/srinath31/ist718_notes/blob/master/markdown/image/DecisionTree.png" width=70%>
</p>

## Problems with Decision Trees

- The problem with decision tree is that there are infinite ways to fit a dataset. 
- This leads to overfitting.

## Ways to solve problems of decision trees

## 1.  Bagging

- Since every time we sample the data the decision tree varies a lot leading to high variance. If we average several random functions, then the variance can be reduced. There is a theory called as wisdom of crowd which says that if you take more and more suggestions from various people, more accurate the decisions would be. For example, in democratic region, one person alone does not vote for a leader. Instead a leader is chosen from a majority of multiple votes.

- This idea is extended to a concept known as Bagging. Bagging is called as Bootstrap Aggregation. 

- Bagging helps in reducing variance

- Tree Bagging: 
We create a bag of train data sets. We train different trees in each of those dataset, then we combine them. 
For classification we take majority vote whereas for regression we take average predicitons.
Also 1/3rd of data is not used for training in bagging since sampling is done with replacement.

NOTE: In Bagging, sampling is done on rows only.

- Below is an example of Bagging:
<p align="center">
<img src="https://github.com/srinath31/ist718_notes/blob/master/markdown/image/Bagging.png" width=70%>
</p>

## 2. Random Forest

- Though bagging reduces variance, it results in high correlation. This problem is solved by random forest. Random forest is a tweak to the boostrapped trees predictions that decorrelate trees. It does this by randomly sampling  f  features during each split when bulding the tree. In this way, each of trees look at different features and become decorrelated. A typical value of   $f = \sqrt{n}$ , where  $𝑝$  is the total number of variables.

- Thus Random Forest helps in reducing the correlation problem arising due to bagging.

NOTE: In Random Forest, sampling is done on both rows as well as columns. An advantage of Random Forest is that it is very hard to overfit. However, the problem is that if you have thousand trees how do we interpret it. Feature Importance helps in how do we try to give a sense of how important the features are, given there are different trees with different paths and branches. One idea is that when we build a tree, we see what features we use for spliting and then how much the split gives in terms of loss gain i.e. how much you reduce the loss. If a feature is higher up the tree the it will reduce loss the most.  we can use to reduce all trees and branches. Higher the feature importance, more help in reducing the loss. In logistic regression there are positive and negative weights which signify the impact of the outcome. However, in feature importance we reduce the loss but don't know how we relate the important features to the outcome.      

## 3. Gradient Boosting

- Boosting grows a model. It first fits a simple model and the next model focuses on samples poorly fit by the previous model. It is a way of adaptively fitting the data. In a sense, boosting does not resample the data.

- While Bagging aims at lowering the variance in the learning process, Boosting aims at reducing the bias.

- Principal of boosting: We combine weak learners, for example we have regression or classification issues, we choose something that gives you just above 50%(weak learner). Idea of boosting is to make each of weak learner learn from mistakes of previous learner. 
