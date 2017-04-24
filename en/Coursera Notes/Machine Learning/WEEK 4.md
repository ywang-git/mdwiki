# Neural Networks: Representation

## Motiations

### Non-linear Hypotheses

Feature set would get too large if we include high order polynomial hypothesis funcitons.

### Neurons and the Brain

universal learning algorithms

## Neural Networks

### Model Representation I

In neural networks, sigmoid function $\frac{1}{1 + e^{-\theta^TX}}$ is used as **activation** function. "theta parameters" are sometimes called "weights".
\\\[
\begin{bmatrix}
x _0\\\
x _1\\\
x _2\\\
\end{bmatrix} \rightarrow [  ] \rightarrow h _\theta(x)
\\\]

input nodes (layer 1) is input layer
layer 2 is hidden layer
layer 3 is output layer

Notation:

$a _i^{(j)} =$ "activation" of unit $i$ in layer $j$

$\Theta^{(j)} =$ matrix of weights controlling function mapping from layer $j$ to layer $j + 1$

\\\[
\begin{bmatrix}
x _0\\\
x _1\\\
x _2\\\
\end{bmatrix} \rightarrow \begin{bmatrix}
a _1 ^{(2)}\\\
a _2 ^{(2)}\\\
a _3 ^{(2)}\\\
\end{bmatrix} \rightarrow h _\theta(x)
\\\]

activation nodes calculation

\\\[
a _1^{(2)} = g(\Theta _{10} ^{(1)} x _0 + \Theta _{11} ^{(1)} x _1 + \Theta _{12} ^{(1)} x _2 + \Theta _{13} ^{(1)} x _3 )\\\
a _2^{(2)} = g(\Theta _{20} ^{(1)} x _0 + \Theta _{21} ^{(1)} x _1 + \Theta _{22} ^{(1)} x _2 + \Theta _{23} ^{(1)} x _3 )\\\
a _3^{(2)} = g(\Theta _{30} ^{(1)} x _0 + \Theta _{31} ^{(1)} x _1 + \Theta _{32} ^{(1)} x _2 + \Theta _{33} ^{(1)} x _3 )\\\
h _\Theta(x) = a _1 ^{(3)} = g(\Theta _{10} ^{(2)} a _0 ^{2} + \Theta _{11} ^{(2)} a _1 ^{2} + \Theta _{12} ^{(2)} a _3 ^{2} + \Theta _{13} ^{(2)} a _3 ^{2} )\\\
\\\]

each layer gets its own matrix of weights, $\Theta^{(j)}$

If network has $s _j$ units in lyaer $j$ and $s _{j + 1}$ units in lyaer $j + 1$, then $\Theta ^{j}$ will be of dimension $s _{j + 1} \times (s _j + 1)$.

$+ 1$ is from "bias nodes" $x _0$ and $\Theta _0 ^{(j)}$.

### Model Representation II

#### Forward propagation: Vectorized implementation

define a new variable $z _k ^{(j)}$ that encompasses the parameters inside our $g$ function. Then:
\\\[
a _1^{(2)} = g(z _1^{(2)})\\\
a _2^{(2)} = g(z _2^{(2)})\\\
a _3^{(2)} = g(z _3^{(2)})\\\
\\\]

for layer j = 2 and node k, the variable z will be:
\\\[
z _k ^{(2)} = \Theta _{k, 0} ^{(1)}x _0 + \Theta _{k, 1} ^{(1)}x _1 + \cdots + \Theta _{k, n} ^{(1)}x _n
\\\]

vector represnetation of $x$ and $z^j$:

\\\[
x =\begin{bmatrix}
x _0\\\
x _1\\\
\cdots\\\
x _n\\\
\end{bmatrix} z^{(j)} = \begin{bmatrix}
z _1 ^{(j)}\\\
z _2 ^{(j)}\\\
\cdots\\\
a _n ^{(j)}\\\
\end{bmatrix}
\\\]


Setting $x = a ^{1}$, then
\\\[
z ^{(j)} = \Theta ^{(j - 1)}a^{(j - 1)}
\\\]



## Applications

### Examples and Intuitions I

\\\[
\begin{bmatrix}
x _0\\\
x _1\\\
x _2\\\
\end{bmatrix} \rightarrow \begin{bmatrix}
g(z^{(2)})
\end{bmatrix} \rightarrow h _\theta(x)
\\\]

Logic AND gate
\\\[
\Theta^{(1)}=[-30\ 20\ 20]
\\\]

Logic OR gate
\\\[
\Theta^{(1)}=[-10\ 20\ 20]
\\\]

### Examples and Intuitions II

Truth table of NOR gate

|$x _1$|$X _2$|$a _1^{(2)}$|$a _2^{(2)}$|$h _\Theta(x)$|
| ---- | ---- | ---- | ---- | ----|
| 0 | 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 0 | 0 |
| 1 | 0 | 0 | 0 | 0 |
| 1 | 1 | 1 | 0 | 1 |

### Multiclass Classfication

result class y:


\\\[
y^{(i)}=\begin{bmatrix}
1\\\
0\\\
0\\\
0\\\
\end{bmatrix},\begin{bmatrix}
0\\\
1\\\
0\\\
0\\\
\end{bmatrix},\begin{bmatrix}
0\\\
0\\\
1\\\
0\\\
\end{bmatrix},\begin{bmatrix}
0\\\
0\\\
0\\\
1\\\
\end{bmatrix},
\\\]

[gimmick: math]()
