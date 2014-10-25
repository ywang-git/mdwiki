#3 Growth of Functions
**asymptotic efficiency**: how the running time of an algorithm increases with the size of input _in the limit_ as the size of the input increases without bound.
___
##3.1 Asymptotic notation
Domains: natrual numbers $$$\mathbb{N}=\left\\{0, 1, 2, …\right\\}$$$

abuse -> real numbers
###Asymptotic notions, functions, and running times
$$$\Theta(n^2) = an^2 + bn + c$$$
####$$$\Theta$$$-notation

$$$\Theta(g(n))=\left\\{f(n):\text{ there exist positive constans }c_1\text{, }c_2\text{, and }n_0\text{ such that }\\\
0 \leq c_1g(n) \leq f(n) \leq c_2g(n) \text{ for all }n \geq n_0\right\\}.$$$

For all $$$n \geq n_0$$$, the function $$$f(n)$$$ is equal to $$$g(n)$$$ to within a constant factor. We say that $$$g(n)$$$ is an **_asymptotically tight bound_** for $$$f(n)$$$.

The definition of $$$\Theta(g(n))$$$ requires  that every member $$$f(n) \in \Theta(g(n))$$$ be **_asymptotically nonegative_**, that is, that $$$f(n)$$$ be nonnegative whenever n is sufficiently large.

####_O_-notation

$$$O(g(n))=\left\\{f(n):\text{ there exist positive constants }c\text{ and }n_0 \text{ such that }\\\
0 \leq f(n) \leq cg(n) \text{ for all } n \geq n_0\right\\}.$$$

####$$$\Omega$$$-notation
$$$\Omega(g(n))=\left\\{f(n):\text{ there exist postive constants }c\text{ and }n_0\text{such that}\\\
0\leq cg(n)\leq f(n)\text{ for all }n\geq n_0 \right\\}.$$$

#####_Theorem 3.1_
For any two functions $$$f(n)$$$ and $$$g(n)$$$, we have $$$f(n)=\Theta(g(n))$$$ if and only if $$$f(n) = O(g(n))$$$ and $$$f(n)=\Omega(g(n))$$$.

####Asymptotic notation in equations and inequalities

####_o_-notation

$$$o(g(n))=\left\\{f(n):\text{ for any positive constant }c>0\text{, there exists a constant }\\\
n_0>0\text{ such that }0\leq f(n)\leq cg(n)\text{ for all }n\geq n_0\right\\}.$$$


\\[\lim_{n \to \infty}\frac{f(n)}{g(n)}=0\\]

####$$$\omega$$$-notation

$$$\omega(g(n))=\left\\{f(n):\text{ for any positive constant }c > 0\text{, there exists a constant }\\\
n_0>0\text{ such that } 0\leq cg(n)<f(n)\text{ for all }n\geq n_0\right\\}.$$$

\\[\lim_{n \to \infty}\frac{f(n)}{g(n)}=\infty\\]

###Comparing functions
####Transtivity:
\\[\\\
f(n)=\Theta(g(n))\text{ and }g(n)=\Theta(h(n))\text{ imply }f(n)=\Theta(h(n)),\\\
f(n)=O(g(n))\text{ and }g(n)=O(h(n))\text{ imply }f(n)=O(h(n)),\\\
f(n)=\Omega(g(n))\text{ and }g(n)=\Omega(h(n))\text{ imply }f(n)=\Omega(h(n)),\\\
f(n)=o(g(n))\text{ and }g(n)=o(h(n))\text{ imply }f(n)=o(h(n)),\\\
f(n)=\omega(g(n))\text{ and }g(n)=\omega(h(n))\text{ imply }f(n)=\omega(h(n)).\\]
####Reflexivity:
\\[\\\
f(n)=\Theta(f(n)),\\\
f(n)=O(f(n)),\\\
f(n)=\Omega(f(n)).\\]
####Symmetry:
\\[f(n)=\Theta(g(n))\text{ if and only if }g(n)=\Theta(f(n)).\\]
####Transpose symmetry:
\\[f(n)=O(g(n))\text{ if and only if }g(n)=\Omega(f(n)),\\\
f(n)=o(g(n))\text{ if and only if }g(n)=\omega(f(n)).\\]

We say that $$$f(n)$$$ is **_asymptotically smaller_** than $$$g(n)$$$ if $$$f(n)=o(g(n))$$$, and $$$f(n)$$$ is **_asymptotically larger_** than $$$g(n)$$$ if $$$f(n)=\omega(g(n))$$$.

##3.2 Standard notations and common functions
###Monotonicity
A function $$$f(n)$$$ is **_monotonically increasing_** if $$$m\leq n$$$ implies $$$f(m)\leq f(n)$$$.

###Floors and ceilings

###Modular arithmetic

###Polynomials
**_polynomial in n of degree d_**
\\[p(n)=\sum_{i=0}^da_in^i.\\]
###Exponentials
For all real constants $$$a$$$ and $$$b$$$ such that $$$a>1$$$,
\\[\lim_{n\to\infty}\frac{n^b}{a^n}=0,\\]
from which we can conclude that
\\[n^b=o(a^n)\\]
###Logarithms
We say that a function $$$f(n)$$$ is **_polylogarithmically bounded_** if $$$f(n)=O(lg^kn)$$$ for some constant $$$k$$$.

We can conclude that
\\[lg^bn=o(n^a)\\]
for any constant $$$a > 0$$$.

###Factorials
\\\[n!=\begin{cases}1&\text{if } n=0,\\\
n\cdot(n-1)!&\text{if }n>0.\end{cases}\\\]

**_Stirling's approximation._**
###Functional iteration
\\\[f^{(i)}=\begin{cases}n&\text{if } i=0,\\\
f(f^{i-1}(n))&\text{if }i>0.\end{cases}\\\]
####The iterated logarithm function
###Fibonacci numbers
\\[F_i=\lfloor\frac{\phi^i}{\sqrt{5}}+\frac{1}{2}\rfloor\\].

