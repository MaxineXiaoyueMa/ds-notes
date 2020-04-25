# Machine Learning Concept

## Algorithms
### Regression
#### Regression Algorithms
1. **Linear Regression**
  **LASSO**
  **Ridge**
2. **Decision Trees**
3. **Random Forest Regressor**
4. **Gradient Boosted Trees Regressor**
5. **Adaboost Regressor**
6. **Support Vector Regression**

#### Regression metrics
1. **MSE**(Mean Squared Error): popular metric for regression models as a loss function, calculates the average of squared error = (y truth - y prediction). Note large error's are penalized much heavier than small errors. Parameters update much faster during graident descent with this loss function at large errors.
2. **RMSE**(Root Mean Squared Error): square root of MSE, but has same unit as predition
3. **MAE**(Mean Absolute Error): caculate the average of the absolute value of error. Note parameter updates the same speed across error range in contrast to MSE due to linear increase of error in loss.
4. **R-Squared**(Coefficient of Determination): the proportion of variance in y that is explained by the features. 1 - SSE(Sum of Squared Errors)/TSS(Total Sum of Squares). Default metric for regression models on sklearn.
5. **Adjusted R-Squared**(Adjusted Coefficient of Determination): like R-Squared, but penalizes the amount of features used in prediction, is always smaller than R-Squared. 1 - (SSE/(n-k))/(TSS/(n-1))

### Classification
#### Classification Algorithms
1. **Naive Bayes Classifier** - generative model P(x, y)
> Essentially, comparing probability of having feature set X conditional on target being positive vs. negative.

P(y|X) = P(y&X) / P(X)
P(1-y|X) = P((1-y)&X) / P(X)
Since the denomenator is the same, compare P(y&X) and P((1-y)&X)

Reference: http://cs229.stanford.edu/notes/cs229-notes2.pdf

2. **Logistic Regression**
3. **Decision Trees**
  1. **Split criteria**:
     1. **Gini Impurity**: the probability of a randomly selected sample is wrongly classified
     2. **Entropy**: the amount of information(surprise) enclosed
  1. **Feature importance**:
     1. **Gini importance**: The average of impurity reduced by each feature
     2. **Permutation importance**: mean accuracy (or any other metrics) reduction due to permuting each features, averaged over all trees.
4. **Random Forest Classifier** - discriminative model P(y|x): Simultaneousely build a forest of trees that each independently make predictions on samples. Subsampling and using only a small group of features add randomness. Each tree can also be limited to control overfitting.
5. **Gradient Boosted Trees**
6. **Adaboost**: Buildling estimators sequentially to lear better from mistakes. Adaptive by giving more weight to samples that were wrong.
     1. initiliaze equal weight 1/# of observations to each observation
     2. iterate:
          1. calculate weighted error
          2. calculate model weight with weighted error
          3. update sample weight with weighted error
          4. build another model with newly weighted samples
     1. calculate final prediction with prediction from each model weighted by their weights:
          1. weighted probability
          2. majority vote
7. **Support Vector Machine**

#### Classification Metrics
1. **ROC Curve**: rank observation from the most likely to least likely, a good separater will have have score
2.**Accuracy**: default metric for classification models, measure how many observations are correctly classified with default threshold 0.5, not a good measure for imbalanced data, or threshold other than 0.5.
3. **Precision-Recall Curve**:


### Unsupervised
#### Clustering
1. **KMeans**: find predetermined number of clusters. It is achieved by first pick cluster centers, then iteratively calculate euclidean distance between observations and cluter centers, assign observations to cluster centers, and recalculate cluster centers by averaging the distances of observations to corresponding cluster centers until convergence.

## Modeling
### Model tuning
1. Random search
2. grid search
3. baysian based optimization:
Reference: https://www.cs.cornell.edu/courses/cs4787/2019sp/notes/lecture16.pdf
