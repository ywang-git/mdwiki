\\[T(n)= \begin{cases} \Theta(1)&\text{if } (n \leq c)\\\
a T(\frac{n}{b})+ D(n) + C(n) &\text{otherwise}\end{cases}\\]

for merge sort

\\[T(n)=\begin{cases}\Theta(1)&\text{if }(n = 1)\\\
2T(\frac{n}{2})+\Theta(n)&\text{if }(n > 1)\end{cases}\\]