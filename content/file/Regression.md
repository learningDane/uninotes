#uni 
Predicting a continuous value rather than a category.

Possible algorithms:
- linear regression
- polynomial regression
- ridge regression
- lasso regression
- decision trees and random forests
- neural networks

The goal is to learn a function $f:X \to Y$ that minimizes the expected loss:
$$
R(f)=\mathbb E_{(x,y) \sim P}[ l(f(x),y) ]
$$

We first have to select a loss function, for single point commons losses are:
- squared loss
- absolute error
- Huber Loss
