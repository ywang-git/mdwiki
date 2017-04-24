# Introduction

## Welcome

### Welcome to Machine Learning

- Grew out of work in AI
- New capability for computers

#### Example

- Database mining
- Applications can't program by hand
- Self-customizing programs
- Understanding human learning (brain, real AI)

### What is Machine Learning?

Two definitions of Machine Learning are offered.

Arthur Samuel described it as: "the field of study that gives computers the ability to learn without being explicitly programmed." This is an older, informal definition.

Tom Mitchell provides a more modern definition: "A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E."

Example: playing checkers.

- E = the experience of playing many games of checkers
- T = the task of playing checkers.
- P = the probability that the program will win the next game.

### Supervised Learning

Example: housing price prediction
linear / (quadratic) second order polynomial

- give the right answers
- regression: predict continuous value

Example: predict tumor type

- classification: discrete valued output

#### infinite number of features / attributes? 
support vector machine: math trick allowing computer to deal with infinite number of features


### Unsupervised Learning
#### clustering algorithm

Google news
Genes categorize


- organize computing clusters
- social network analysis
- market segmentation
- astronomical data analysis

#### cocktail party problem

$[W, s, v] = svd((repmat(sum(x.*x,1),size(x,1),1).*x)*x');$

Octave

# Linear Regression with One Variable

## Model and Cost Function

### Model Representation

Housing Price

Fitting a Line

Training set of housing prices

Notation:

`m` = number of training examples
`x`'s = input variable / features
`y`'s = output variable / "target" variable"

$(x, y)$

x -> hypothesis -> estimated value of y

How do we represent h?

$h_\theta(x) = \theta_0 + \theta_1x$ (Univariabte linear regression)


### Cost Function

Hypothesis: $h_\theta(x) = \theta_0 + \theta_1x$

Parameters: $\theta_i$

choose $\theta_0$, $\theta_1$ so that $h_\theta(x)$ is close to $y$ for our training examples $(x, y)$

minimize($\theta_0, \theta_1$) $\frac{1}{2m}\sum^{m}_{i=1}(h_\theta(x^{(i)}) - y^{(i)})^2)$

Cost Function: $J(\theta_0, \theta_1)$ (squared error function)

also called "mean squared error", the mean is halved as a convenience for the computation of the gradient descent, as the derivative term of the square function will cancel out the $\frac{1}{2}$ term.

### Cost Function - Intuition I & II
contour plot

## Parameter Learning

### Gradient Descent
minimize general function

Given function: $J(\theta_0, \theta_1)$
Goal: $\min_{\theta_0, \theta_1}J(\theta_0, \theta_1)$

Outline:

* Start with some $\theta_0, \theta_1$
* Keep changing $\theta_0, \theta_1$ to reduce $J(\theta_0, \theta_1)$ until we hopefullly end up at a minimum

Property: picking different initial values may lead to different local minimum value of the cost function

### Gradient descent algorithm

`repeat until convergence {`
    $\theta_j := \theta_j - \alpha\frac{\partial }{\partial \theta_0}J(\theta_0, \theta_1)$ `(for j = 0 and j = 1)`

`}`

$\alpha$: learning rate, controls how large of the step we are taking

correct: simultaneous update

### Gradient Descent Intuition

* If $\alpha$ is too small, gradient descent can be slow.
* If $\alpha$ is too large, gradient descent can overshoot the minimum. It may fail to converge, or even diverge.

Gradient descent can converge to a local minimum, even with the learning rate $\alpha$ fixed. As we approach a local minimum, gradient descent will automatically take smaller steps. So no need to decrease $\alpha$ over time.

### Gradient Descent for Linear Regression


repeat until convergence: {
$\theta_0 := \theta_0 - \alpha\frac{1}{m}\sum\limits_{i=1}^m(h_\theta(x_i) - y_i)$

$\theta_1 := \theta_1 - \alpha\frac{1}{m}\sum\limits_{i=1}^m((h_\theta(x_i) - y_i)x_i)$

}

cost function for linear regressions is always a convex function, which only has global minimium but not local minimum.

normal equation method: solve minimum cost function, but does not scale well for large data sets as gradient descent

\\[\frac{\partial}{\partial \theta_j}J(\theta) = \frac{\partial}{\partial \theta_j} \frac{1}{2}(h_\theta(x) - y)^2 = 2 * \frac{1}{2}(h_\theta(x) - y) * \frac{\partial}{\partial \theta_j}(h_\theta(x) - y) = (h_\theta(x) - y) * \frac{\partial}{\partial \theta_j}(\sum\limits_{i=0}^{n}\theta_ix_i - y) = (h_\theta(x) - y)x_j\\]

Batch Gradient Descent
"Batch": Each step of gradient descent uses all the training examples.

[gimmick: math]()
