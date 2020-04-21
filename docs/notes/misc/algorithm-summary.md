## Regression
### Linear Regression
#### LASSO
#### Ridge

### Decision Trees

### Random Forest Regressor

### Gradient Boosted Trees Regressor

### Adaboost Regressor

### Support Vector Regression



## Classification

### Naive Bayes Classifier - generative model P(x, y)
> Essentially, comparing probability of having feature set X conditional on target being positive vs. negative.

P(y|X) = P(y&X) / P(X)
P(1-y|X) = P((1-y)&X) / P(X)
Since the denomenator is the same, compare P(y&X) and P((1-y)&X)

Reference: http://cs229.stanford.edu/notes/cs229-notes2.pdf

### Logistic Regression

### Decision Trees
1. Split criteria:
   1. Gini Impurity: the probability of a randomly selected sample is wrongly classified
   2. Entropy: the amount of information(surprise) enclosed
1. Feature importance:
   1. Gini importance: Gini impurity reduction due to each feature from each tree, averaged over all trees
   2. Permutation importance: mean accuracy (or any other metrics) reduction due to permuting each features, averaged over all trees

### Random Forest Classifier - discriminative model P(y|x)


### Gradient Boosted Trees

### Adaboost

### Support Vector Machine
