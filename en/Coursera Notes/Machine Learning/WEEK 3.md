# Logistic Regression

## Classficiation and Representation

### Classfication

Simply using linear regression with features labeled with 0 and 1, and choosing 0.5 as threshold does not work well for classfication problems.

Binary classificaiton problem.

### Hypothesis Representation

Sigmoid Function / Logistic Function

\\\[
h_\theta(x) = g(\theta^Tx)\\\
z = \theta^Tx\\\
g(z) = \frac{1}{1 + e^{-z}}
\\\]

The function $g(z)$ maps any real number to the (0, 1) interval.

$h_\theta(x) = $ estimated probability that y = 1 on input x

\\\[
h_\theta(x) = P(y = 1|x;\theta) = 1 - P(y = 0|x;\theta)\\\
P(y = 0|x;\theta) + P(y = 1|x;\theta) = 1
\\\]

### Decision Boundary

Decision boundary is the visualization of the hypothesis function before applying the Sigmoid Function. It is a curve that separates the data sets that would be predicted to be 0 and 1.

\\\[
h _\theta(x) \geq 0.5 \rightarrow y = 1\\\
h _\theta(x) < 0.5 \rightarrow y = 1
\\\]

The property of the logistic function $g$:
\\\[
g(z) \geq 0.5  when  z \geq 0
\\\]

Remember: 

\\\[
z = 0, e^0 = 1 \Rightarrow g(z) = 1 / 2\\\
z \rightarrow \infty, e^{-\infty} \rightarrow 0 \Rightarrow g(z) = 1\\\
z \rightarrow -\infty, e^{\infty} \rightarrow \infty \Rightarrow g(z) = 0
\\\]

## Logistic Regression Model

### Cost Function

The cost funtion for linear regression cannot be used due to lack of global optimal (non-convex). [it is probably not logical correct since we are not penalizing the wrong prediciton]


\\\[
J(\theta) = \frac{1}{m}\sum\limits^m_{i=1}Cost(h _\theta(x^{(i)}), y^{(i)})\\\
Cost(h _\theta(x), y) = - \log(h _\theta(x)) if y = 1\\\
Cost(h _\theta(x), y) = - \log(1 - h _\theta(x)) if y = 0
\\\]

Effect
\\\[
Cost(h _\theta(x), y) = 0 if h _\theta = y\\\
Cost(h _\theta(x), y) \rightarrow \infty if y = 0 and h _\theta(x) \rightarrow 1\\\
Cost(h _\theta(x), y) \rightarrow \infty if y = 1 and h _\theta(x) \rightarrow 0\\\
\\\]

### Simplified Cost Function and Gradient Descent

Simplified Cost Function:
\\\[
Cost(h _\theta(x), y) = -y \log(h _\theta(x)) - (1 - y)\log(1 - h _\theta(x))
\\\]

Entire cost function:
\\\[
J(\theta) = - \frac{1}{m}\sum\limits_{i=1}^{m}[y^{(i)}\log(h _\theta(x^{(i)})) + (1-y^{(i)})\log(1 - h _\theta(x^{(i)}))]
\\\]

Vectorized implementation:
\\\[
h=g(X\theta)\\\
J(\theta) = \frac{1}{m}\cdot(-y^T\log(h) - (1 - y)^T\log(1-h))
\\\]

#### Gradient Descent

Repeat

\\\[
\theta _j := \theta _j - \frac{\alpha}{m}\sum\limits _{i=1}^{m}(h _\theta(x^{(i)}) - y^{(i)})x _j^{(i)}
\\\]

Vectorize
\\\[
\theta := \theta - \frac{\alpha}{m}X^T(g(X\theta) - \overrightarrow{y})
\\\]

### Advanced Optimization

"Conjugate gradient", "BFGS", and "L-BFGS" are more sophisticated, faster ways to optimize θ that can be used instead of gradient descent. 

Function returns $J(\theta)$ and $\frac{\partial}{\partial\theta _j}J(\theta)$

```
function [jVal, gradient] = costFunction(theta)
  jVal = [...code to compute J(theta)...];
  gradient = [...code to compute derivative of J(theta)...];
end
```

Octave command to calculate / optimize:

```
options = optimset('GradObj', 'on', 'MaxIter', 100);
initialTheta = zeros(2,1);
   [optTheta, functionVal, exitFlag] = fminunc(@costFunction, initialTheta, options)
```

## Multiclass Classification
### Multiclass Classification: One-vs-all

Train a logistic regression classifier hθ(x) for each class￼ to predict the probability that ￼ ￼y = i￼ ￼.

To make a prediction on a new x, pick the class ￼that maximizes hθ(x)

# Regularization
## Solving the Problem of Overfitting

### The Problem of Overfitting

- Underfitting / high bias: when the form of our hypothesis funciton h maps pooerly to the trend of the data. It is usually caused by a function that is too simple or uses too few features.
- Overfitting / highf variance: is caused by a hypothesis function that fits the available data but does not generalize well to predict new data. It is usually caused by a complicated function that creates a lot of unnecessary curves and angles unrelated to the data.

Two main options to address the issue of overfitting:

1. reduce the number of features
	- manually select which features to keep
	- use a model selection algorithm
2. regularization
   - keep all the features, but reduce the magnitude of parameters $\theta_j$
   - regularization works well when we have a lot of slightly useful features
 
### Cost function
 
\\\[
min _\theta \frac{1}{2m}[\sum\limits^{m} _{i = 1} (h _\theta(x^{(i)}) - y^{(i)})^2 + \lambda \sum\limits^{n} _{j=1} \theta _j^2]
\\\]

### Regularized Linear Regression

#### Gradient Descent
\\\[
Repeat \\\{\\\
\theta _0 := \theta _0 - \alpha \frac{1}{m} \sum \limits^{m} _{i=1} (h _\theta(x^{(i)}) - y^{(i)})x _0^{(i)}\\\
\theta _j := \theta _j - \alpha [\frac{1}{m} \sum \limits^{m} _{i=1} (h _\theta(x^{(i)}) - y^{(i)})x _j^{(i)} + \frac{\lambda}{m}\theta _j] j \in \\\{1, 2 \dots n\\\}\\\
\\\}\\\
\\\]

Can be also represented as:

\\\[
\theta _j := \theta _j(1 - \alpha \frac{\lambda}{m}) - \alpha \frac{1}{m} \sum \limits^{m} _{i=1} (h _\theta(x^{(i)}) - y^{(i)})x _j^{(i)}\\\
\\\]

where $(1 - \alpha \frac{\lambda}{m})$ is less than 1

#### Normal Equation

\\\[
\theta = (X^TX + \lambda \cdot L)^{-1}X^Ty\\\
where L = \begin{bmatrix}
0\\\
&1\\\
&&1\\\
&&&\ddots\\\
&&&&1\\\
\end{bmatrix}
\\\]

$(X^TX + \lambda \cdot L)$ is also always invertible.

### Regularized Logistic Regression

#### Cost Function
\\\[
J(\theta) = -\frac{1}{m}\sum\limits^{m} _{i=1}[y^{(i)}log(h _\theta(x^{(i)})) + (1 - y^{(i)})log(1 - h _\theta(x^{(i)}))]
\\\]

regularize:
\\\[
J(\theta) = -\frac{1}{m}\sum\limits^{m} _{i=1}[y^{(i)}log(h _\theta(x^{(i)})) + (1 - y^{(i)})log(1 - h _\theta(x^{(i)}))] + \frac{\lambda}{2m}\sum\limits^{n} _{j=1}\theta^2 _j
\\\]

excluding the bias term, \theta0

[gimmick: math]()
