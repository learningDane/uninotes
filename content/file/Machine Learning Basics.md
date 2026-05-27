#uni 
[[Algebra Lineare]]
$$
\begin{cases}
y = f(t)
\\
t=g(x)
\end{cases}
\implies \frac{dy}{dx}=\frac{dy}{dt} \cdot \frac{dt}{dx}
$$

>[!quote] "What we want is a machine that can learn from experience"
>Alan Turing - 1947
# Introduction
Evolution:
1. Neural Networks
2. Machine Learning
3. Deep Learning

Machine Learning is a subset of Artificial Intelligence that enables systems to learn and improve from experience without being explicitly programmed. 

Machine learning finds patterns hidden in large amounts of data.
# Workflow
1. data collection
2. data preprocessing
3. feature engineering: extract meaningful features
4. model selection: choose appropriate algorithm
5. training
6. evaluation
7. optimization
8. deployment
9. monitoring
# Basic procedure
1. Study the data
2. select a model or learning algorithm
3. train on the available data and assess performance
4. apply the model to make predictions on new cases
# Common problems
- insufficient quantity of training data
- non-representative and poor-quality training data
- irrelevant features
- **overfitting** the training data: the model is too complex relative to the amount and noisiness of data. Solutions:
	- simplify the model (or add **regularization**)
	- add more data
	- reduce the noise and the outliers (data preparation)
- **underfitting** the training data: the model is too simple
# Evaluation of ML models
The only way to evaluate a model is trying it on new cases:
- always evaluate on data that the model hasn't seen during training
- use appropriate metrics for your problem
- consider both statistical and practical performance
- understand the model's strengths and weaknesses
## Common approaches
- train/test split
- cross-validation
- evaluation metrics
- confusion matrix
- learning curves
### Train/Test Split
We have to split the data to provide an unbiased evaluation: one set (70-80%) for training and one set (20-30%) to evaluate performance.

The error on the test set is called **generalization error** or **out-of-sample error**. 

If the training error is low and generalization error is high, then *overfitting* occurs: we have to change **hyperparameters** (HOW the model learns and how complex it is).

Sometimes we divide the training set in another split: training set and validation set.
The validation set gets used to tune hyperparameters.

# Types of machine learning
## Supervised learning
Learn from labeled examples to predict outcomes for new data: the system is provided with input-output pairs, the model needs to learn the mapping function from inputs to outputs.
Once trained it can make predictions on new, unseen inputs.

This requires labeled data.

Supervised Learning is formalized within the [[Statistical Learning Theory]] framework, developed by Vladimir Vapnik and Alexey Chervonenkis (Vapnik & Chervonenkis, 1971).
### Generalization and Complexity

- Bias: represents systematic error
- Var: represents estimation variance
- $\sigma ^2$: irreducibile error
### Classification
Predict a category: discrete.
### Regression
Predict a quantity: continuous.
## Unsupervised learning
There is no correct answers to learn from.

Useful for **novelty detection**: find new instances that look different.
## Semi-supervised learning
## Deep learning
Use neural networks with multiple layers.

Deep learning allows computational models that are composed of multiple
processing layers to learn representations of data with multiple levels of abstraction.
## Reinforcement learning
Learn through trial and error with rewards: find the best strategy (known as policy) to get the most reward.

This is the last resort, use this only when there is no available data.
## Transfer learning
Apply knowledge from one task to another.

Use knowledge from an already trained system to perform learning on a new task or the same with a different data distribution.
## Other categorizations
Batch learning (or offline learning) vs Incremental learning
- lots of data in one shot
- Train the system incrementally by feeding data instances sequentially.

Better to use less data sequentially than lots of data all in one time.

Instance-based learning vs model-based learning
- the system uses a similarity measure to compare new cases to the learned examples
- build a model of the learned examples and the use that model to make predictions