# Machine Learning Concept

## Algorithms
### Regression
#### Regression Algorithms
1. **Linear Regression**
  **LASSO**: regularization term is the L1 norm sum of absolute values of parameters
  **Ridge**: regularization term is the L2 norm - sum of squared values of parameters
2. **Decision Trees**
3. **Random Forest Regressor**:
4. **Gradient Boosted Trees Regressor**
5. **Adaboost Regressor**:
6. **Support Vector Regression**: find the hyperplane such that all observations fall in the band. Support vectors are the vectors that are on the edge of the band.

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
1. **ROC-AUC**: Average rank (position) of positive items in a sequence of negative items. A perfect ranker that ranks all positive items higher than negative ones has value 1. Random guess has value 0.5.

To plot:
    1. Rank observation from the most likely to least likely,
    2. Plot FPR(**F**alse **P**ostive **R**ate = False Positive/Total False) on the horizontal axis, Recall on the vertical axis.
    3. Move up on recall for each True Postive item, and move right on FPR for each False Positive.

Below is a great illustration from [a great article](http://fouryears.eu/2011/10/12/roc-area-under-the-curve-explained/comment-page-1/) on ROC-AUC curve, fantastic source.
![ROC-AUC](http://fouryears.eu/2011/10/12/roc-area-under-the-curve-explained/roc1-2/)
credit: Konstantin Tretyakov
2.**Accuracy**: default metric for classification models, measure how many observations are correctly classified with default threshold 0.5, not a good measure for imbalanced data, or threshold other than 0.5.
3. **Precision-Recall Curve**:


### Unsupervised
#### Clustering
1. **KMeans**: find predetermined number of clusters. It is achieved by first pick cluster centers, then iteratively calculate euclidean distance between observations and cluter centers, assign observations to cluster centers, and recalculate cluster centers by averaging the distances of observations to corresponding cluster centers until convergence.
2. **Cluster Measures**:
     1. cluster similarities: adjusted Rand Index (pairs that two clusering agress over total pairs adjusted for randomness)
     2. how good the clusters are: silhouette score (using mean distance from each point to other points within the same cluster and mean distance from each point to points outside the same clusters. Good clustering result in small distance within cluster, and large distance outside cluster, final measure is close to 1.)

Reference:
- https://www.datarevenue.com/en-blog/building-a-city-recommender-for-nomads
- https://towardsdatascience.com/beginners-recommendation-systems-with-python-ee1b08d2efb6
- https://medium.com/data-science-101/movie-recommendation-system-content-filtering-7ba425ca0920
- https://towardsdatascience.com/how-did-we-build-book-recommender-systems-in-an-hour-the-fundamentals-dfee054f978e
- https://www.kaggle.com/gspmoreira/recommender-systems-in-python-101
- https://towardsdatascience.com/building-a-content-based-recommender-system-for-hotels-in-seattle-d724f0a32070

## Modeling
### Model tuning
1. Random search
2. grid search
3. bayesian based optimization: "smartly" sample hyperparameter space by learning from previous trials. Gaussian process to poximate
Reference: https://www.cs.cornell.edu/courses/cs4787/2019sp/notes/lecture16.pdf
https://www.arxiv-vanity.com/papers/1012.2599/

## Recommender System
Prediction of personal preference of items, match between user and product/item/experience/tactics/friend/mate.

- type:
    - **random**: random select, no "cold start",
    - **most popular**: require some interaction data
    - **Content Based**: robust to "cold start", recommendation based on similarities between items, i.e., "I like item A, B is similar to A, so, I probably like B", e.g., "if you bought this, you may also like these...", need one user interaction to start.
    - **Collaborative Filtering**: recommendation based on similarities between personal tasts, e.g., he and I have similar tastes, so, if he likes it, then I will probably like it.
        - **Memory based**: uses entire raitngs table, KNN
            - **Item based**: guess my rating for A by finding items most similar to A and calculate a (weighted) average of my ratings for most similar items. The similarity between items A & B is calculated with ratings from users who have rated A & B both.
                - **vs. content based**: item based CF uses implicit similarity between items with interaction/taste as medium, content based uses direct similarity between items
            - **User based**: e.g. "customers like you also likes"
        - **Model Based**:
            - **Matrix Factorization**: SVD
                - SGD (stochastic gradient descent)
                - ALS (alternating Least Squares)
            - **Deep Learning**
        - **Hybrid**: Matrix Factorization + User/Item metadata, e.g., lightFM
- similarity measures:
    - **cosine similarity**: dot product devided by the product of the norm of both vectors, linear kernel if vectors are already taken the norm in sklearn
- metric:
    - **MAP@N**: getting all N items recomded correctly scores 1 per AP@N. Getting more right per N is better, and getting right ealier is better. sum (Precision@k * change in Recall@k) for k in N.

**Reference**:
- http://fastml.com/evaluating-recommender-systems/
- https://web.stanford.edu/class/cs276/handouts/EvaluationNew-handout-6-per.pdf
- lightFM official paper https://arxiv.org/pdf/1507.08439.pdf
-

## Natural Language Processing (NLP)
0. **Preprocessing**:
     1. **Tokenization**:
     2. **Normalization**:
          1. stemming: running -> run
          2. lemmatization: better -> good
          3.
     3. **Substitution**:
1. **Feature Extraction**: vectorization = text -> numerical transformation
     1. **Bag of words**: tokenizing, counting, (normalizing)
     2. **tfidf**: term weighting, term frequency (tf) times inverse document frequency (idf). idf is calculated as the log of number of documents devided by number of documents containing word, the more common the word, the less informational it is.
          1. **n_gram**: order matters, 'like', and 'not like' mean opposite things, to preserve order, keep n_gram = 3
          2. **stop_words**: common words that don't add information: the, an, is, etc.

## Dimensionaility reduction
1. **PCA**: Project high dimensional data on to smaller subspace that keeps most of the information or variance.
     1. **LSA - NLP**: when applied in NLP tasks, it can be called as Latent semantic Analysis. A good example can be found here: https://www.stat.cmu.edu/~cshalizi/uADA/12/lectures/ch18.pdf
     2. **Components loadings**: how does each variable project on to the Principle Components can help us understand the PCs better.
