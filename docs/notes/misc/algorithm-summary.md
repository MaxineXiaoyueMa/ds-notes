# Machine Learning Concept 

## Regression
### Regression Algorithms
1. **Linear Regression**
  **LASSO**
  **Ridge**
2. **Decision Trees**
3. **Random Forest Regressor**
4. **Gradient Boosted Trees Regressor**
5. **Adaboost Regressor**
6. **Support Vector Regression**

### Regression metrics
1. **MSE**(Mean Squared Error)
2. **RMSE**(Root Mean Squared Error)
3. **MAE**(Mean Absolute Error)
4. **R-Squared**(Coefficient of Determination)
5. **Adjusted R-Squared**(Adjusted Coefficient of Determination)


## Classification
### Classification Algorithms
1. **Naive Bayes Classifier** - generative model P(x, y)
> Essentially, comparing probability of having feature set X conditional on target being positive vs. negative.

P(y|X) = P(y&X) / P(X)
P(1-y|X) = P((1-y)&X) / P(X)
Since the denomenator is the same, compare P(y&X) and P((1-y)&X)

Reference: http://cs229.stanford.edu/notes/cs229-notes2.pdf

2. **Logistic Regression**
3. **Decision Trees**
  1. Split criteria:
     1. Gini Impurity: the probability of a randomly selected sample is wrongly classified
     2. Entropy: the amount of information(surprise) enclosed
  1. Feature importance:
     1. Gini importance: Gini impurity reduction due to each feature from each tree, averaged over all trees
     2. Permutation importance: mean accuracy (or any other metrics) reduction due to permuting each features, averaged over all trees.
4. **Random Forest Classifier** - discriminative model P(y|x)
5. **Gradient Boosted Trees**
6. **Adaboost**
7. **Support Vector Machine**

### Classification Metrics

## Unsupervised
