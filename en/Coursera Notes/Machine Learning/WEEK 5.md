# Nerual Networks: Learning

## Cost Function and Backpropagation

### Cost Function

Notation:

* $L$ = total number of layers in the network
* $s _l$ = number of units (not counting bias unit) in layer $i$
* $K$ = number of output unit / classes

$h _{\Theta}(x) _k$ - a hypothesis that results in the $k ^{th}$ output.

Cost function:

\\\[
J(\Theta) = -\frac{1}{m}\sum\limits _{i = 1} ^m\sum\limits _{k = 1} ^{K}[y _k ^{(i)} \log((h _\Theta(x ^{(i)})) _k) + (1 - y _k ^{(i)}) \log(1 - (h _\Theta(x ^{(i)})) _k))] + \frac{\lambda}{2m}\sum\limits _{l = 1} ^{L - 1}\sum\limits _{i = 1} ^{s _l}\sum\limits _{j = 1} ^{S +l + 1}(\Theta _{j, i} ^{(l)}) ^2
\\\]

Note:

* the double sum simply adds up the logistic regression costs calculated for each cell in the output layer
* the triple sum simply adds up the squares of all the individual Θs * in the entire network.
* the i in the triple sum does **not** refer to training example i

### Backpropagation Algorithm


Training set $\{(x ^{(1)}, y ^{(1)}), \dots, (x ^{(m)}, y ^{(m)})\}$

Set $\Delta _{ij}^{(l)} = 0$ (for all $l, i, j$)

For $i = 1$ to $m$

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set $a ^{(1)} = x ^{(i)}$

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Perform forward propagation to compute $a ^(l)$ for $l = 2, 3, \dots, L$

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Using $y ^{(i)}$, compute $\delta ^{(L)} = a ^{(L)} - y ^{(i)}$

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Compute $\delta ^{(L - 1)}, \delta ^{(L - 2)}, \dots, \delta ^{(2)}$

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$\Delta _{ij} ^{(l)} := \Delta _{(ij)} ^{(l)} + a _j ^{(l)} \delta _i ^{(l + 1)}$

$D _{ij} ^{(l)} := \frac{1}{m} \Delta _{ij} ^{(l)} + \lambda\Theta _{ij} ^{(l)}$ if $j \neq 0$

$D _{ij} ^{(l)} := \frac{1}{m} \Delta _{ij} ^{(l)} + \lambda\Theta _{ij} ^{(l)}$ if $j = 0$

$\frac{\partial}{\partial \Theta _{ij} ^{(l)}}J(\Theta) = D _{ij} ^{(l)}$

### Backpropagation Intuition

## BackPropagation in Practice

### Implementation Note: Unrolling Parameters

```
thetaVector = [ Theta1(:); Theta2(:); Theta3(:); ]
deltaVector = [ D1(:); D2(:); D3(:) ]
```

```
Theta1 = reshape(thetaVector(1:110),10,11)
Theta2 = reshape(thetaVector(111:220),10,11)
Theta3 = reshape(thetaVector(221:231),1,11)
```

### Gradient Checking

\\\[
\frac{\partial}{\partial\Theta _j}J(\Theta)\approx\frac{J(\Theta _1, \dots, \Theta _j + \epsilon, \dots, \Theta _n) - J(\Theta _1, \dots, \Theta _j - \epsilon, \dots, \Theta _n)}{2\epsilon}
\\\]

```
epsilon = 1e-4;
for i = 1:n,
  thetaPlus = theta;
  thetaPlus(i) += epsilon;
  thetaMinus = theta;
  thetaMinus(i) -= epsilon;
  gradApprox(i) = (J(thetaPlus) - J(thetaMinus))/(2*epsilon)
end;

```

Once you have verified once that your backpropagation algorithm is correct, you don't need to compute gradApprox again. The code to compute gradApprox can be very slow.

### Random initialization

Initializing all theta weights to zero does not work with neural networks. When we backpropagate, all nodes will update to the same value repeatedly. Instead we can randomly initialize our weights for our $\Theta$ matrices using the following method:

If the dimensions of Theta1 is 10x11, Theta2 is 10x11 and Theta3 is 1x11.

```
Theta1 = rand(10,11) * (2 * INIT_EPSILON) - INIT_EPSILON;
Theta2 = rand(10,11) * (2 * INIT_EPSILON) - INIT_EPSILON;
Theta3 = rand(1,11) * (2 * INIT_EPSILON) - INIT_EPSILON;
```

[gimmick: math]()
