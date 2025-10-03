# Chapter7

# Majority Voting vs Individual Classifiers

When we use a single classifier like Logistic Regression, Decision Tree, or KNN, it makes predictions based only on its own way of looking at the data. Each model has its strengths and weaknesses, so it can make mistakes on certain examples.

A majority voting classifier combines several different models and makes a prediction based on what most of them say (or averages their probabilities). This usually leads to better performance because the errors of one model can be corrected by the others.

## Why ensembles usually do better:

They mix different models that make different kinds of mistakes.

They reduce variability, meaning they are less likely to be thrown off by unusual or noisy data.

They tend to be more reliable and robust overall.

## When ensembles might not help:

If all the models are weak or very similar, the ensemble won’t improve much.

If one poor model has too much influence, it can actually lower accuracy.

Adding many similar models just increases complexity without giving any real benefit.

## Bagging Analysis:

Adding more trees usually makes the model more stable and accurate, because averaging over many trees reduces the impact of any single tree’s mistakes.

However, after a certain point (around 100–500 trees), adding more trees doesn’t really improve performance but just makes the model slower to train.

## Bootstrap sampling vs using the entire dataset:

With bootstrap sampling (bootstrap=True), each tree is trained on a random subset of the data (with replacement). This makes each tree a little different, which is important for the ensemble to work well.

If you train all trees on the entire dataset, they all become very similar. This reduces the benefits of bagging because the trees are making the same mistakes.

## Why bagging reduces overfitting:

A single decision tree can easily overfit, meaning it memorizes the training data—including noise and outliers.

Bagging trains many trees on slightly different subsets and then averages their predictions. This reduces the influence of noisy data, lowers variance, and produces predictions that are more stable and reliable.


# AdaBoost Insights:

Learning rate: Controls how much each tree counts. A higher rate fits faster but can overfit and a lower rate learns slower but often generalizes better.

Error convergence: The test error goes down at first because AdaBoost is learning useful patterns. But after many iterations, it starts focusing too much on hard or noisy points that can’t be separated well. This makes the model overfit the training data

Decision stumps: Simple trees with one split work well because AdaBoost combines many of them, letting each fix mistakes from the previous ones.

# Comparative Performance on Iris Dataset:

Majority Voting classifier performed best (0.97), outperforming the individual models. Its strength comes from combining multiple classifiers, which balances their weaknesses and reduces errors.

## Relation of Random Forest to Bagging:

Random Forest is essentially bagging applied to decision trees, but with an extra twist: each tree considers only a random subset of features when splitting. This adds more diversity between trees, improving performance.

## Choosing an ensemble method:

Majority Voting: Good when you have different types of models and want to combine their strengths.

Bagging / Random Forest: Best when using unstable models like decision trees, to reduce overfitting.

AdaBoost: Useful when you want to focus on hard-to-classify samples, but it’s more sensitive to noise.

# Practical Considerations:

computational trade-offs: Bagging and Random Forest are parallelizable across estimators. AdaBoost is sequential (each iteration depends on previous weights). Ensemble size increases training time roughly linearly.

How ensemble size affect the bias-variance tradeoff: Increasing ensemble size typically reduces variance (especially with bagging/forest) and may slightly affect bias (depending on base learner). AdaBoost can reduce both bias and variance by focusing learners where needed.

## Real-world scenarios:

Voting: Best when you already have a few strong, different models (e.g. a logistic regression, a decision tree, and a KNN) and you want to combine their strengths.

Bagging / Random Forest: Great when your data is messy and high-dimensional (e.g. medical records, finance, or e-commerce). Works well as a strong general-purpose model.

AdaBoost: Useful when you want to squeeze out extra accuracy on relatively clean data, like text classification or spam detection. Not great if your data is very noisy.

