# Linear Regression with Multiple Variables

## Multivariate Linear Regression

### Mutliple Features

Notation:

* m = the number of training exmaples
* $n$ = $|x^{(i)}|$; (the number of features)
* $x^{(i)}$ = input (features) of $i^{th}$ training example.
* $x_j^{(i)}$ = value of feature $j$ in $i^{th}$ training example.

$h_\theta(x) = \begin{bmatrix}\theta_0 \theta_1 \dots \theta_n\end{bmatrix}\begin{bmatrix}x_0\\
x_1\\
\dots\\
x_n\end{bmatrix} = \theta^Tx
$

asume $x_0^{(i)} = 1$ for $(i \in 1, \dots, m)$.

### Gradient Descent for Multiple Variables

repeat until convergence: {

$\theta_j := \theta_j - \alpha\frac{1}{m}\sum\limits_{i=1}^m(h_\theta(x^{(i)}) - y^{(i)}) \cdot x_j^{(i)}$ for $j := 0\dots n$

}

### Gradient Descent in Practice I - Feature Scaling
Idea: Make sure features are on a similar scale
Goal: to speed up gradient descent

* Feature Scaling: 
Get every feature into aproximately a $ -1 \leq x_i \leq 1$ range.

* Mean normalization

Replace $x_i$ with $x_i - \mu_i$ to make features have approximately zero mean (Do not apply to $x_0=1$).

$x_i := \frac{x_i - \mu_i}{s_i}$

$\mu_i$ is the average of all the values for feature (i)
$s_i$ is the range of values (max - min), or $s_i$ is the standard devaiation

### Gradient Descent in Practice II - Learning Rate

Make sure gradient descent is working correctly: plot cost function over number of iterations.

convergence test: declare convergence if $J(\theta)$ decreases by less that $10^{-3}$ (it is harder to choose this threshold value)

If $J(\theta)$ increases, try to use smaller $\alpha$

### Features and Polynomial Regression
We can improve our features and the form of our hypothesis function in a couple different ways.

We can combine multiple features into one. For example, we can combine x1 and x2 into a new feature x3 by taking x1⋅x2.


Polynomial regression

We can change the behavior or curve of our hypothesis function by making it a quadratic, cubic or square root function (or any other form).

For example, if our hypothesis function is hθ(x)=θ0+θ1x1 then we can create additional features based on x1, to get the quadratic function hθ(x)=θ0+θ1x1+θ2x21 or the cubic function hθ(x)=θ0+θ1x1+θ2x21+θ3x31

One important thing to keep in mind is, if you choose your features this way then feature scaling becomes very important.

```
the cost function for multivariate linear regression is a generalization of the single variable linear regression
the cost function can be represented as vector multiplication
feature scaling / mean normalization can make gradient descent run faster
choosing learning rate carefully, larger learning rate can let the cost function increase, but smaller learning rate can be slow; choosing smaller alpha should always make cost function decrease
use insight to feature to create new features out of combination or calculation, the result would be polynomial regression
```



### Normal Equation

Alternative to Gradient Descent

$\theta = (X^TX)^{-1}X^Ty$

There is no need to do feature scaling with the normal equation.
The following is a comparison of gradient descent and the normal equation.

| __Gradient Descent__ | __Normal Equation__ |
| ---- | ---- |
| Need to choose alpha | No need to choose alpha |
| Needs many iterations | No need to iterate |
| $O(kn^2)$ | $O(n^3)$, need to calculate inverse of $XTX$ |
| Works well when n is larege | Slow if n is very large |

In practice, when n exceedes 10,000 it might be a good time to go from a normal solution to an iteractive process.

### Normal Equation Noninvertibility

When implementing the normal equation in octave we want to use the 'pinv' function rather than 'inv'. The 'pinv' function will give you a value of $\theta$ even if $X^TX$ is not invertable.

Common cause for $X^TX$ not invertible:

| Cause | Solution |
|----|----|
| Redundant features, where two features are very closely related (i.e. they are linearly dependent)|deleting a feature that is linearly dependent with another |
| Too many features (e.g. $m \leq n$(. In this case, delete some features or use "regularization" (to be explained in a later lesson).| deleting on or more features when there are too many features |

[gimmick: math]()
