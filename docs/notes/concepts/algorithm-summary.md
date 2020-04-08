## Classification

#### Naive Bayes Classifier
Essentially, comparing probability of having feature set X conditional on target being positive vs. negative.

P(y|X) = P(y&X) / P(X)
P(1-y|X) = P((1-y)&X) / P(X)

Ultimately, compare P(y&X) and P((1-y)&X)

**Reference:**
[cs229 notes on generative models](http://cs229.stanford.edu/notes/cs229-notes2.pdf)
