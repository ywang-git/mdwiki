\\[\sum_{h=0}^{\lfloor lg n\rfloor}\lceil\frac{n}{n^{h+1}}\rceil O(h) = 
O\left(n\sum\_{h=0}^{\lfloor lg n\rfloor}{\frac{h}{2^h}}\right).\\]


\\[\sum_{h=0}^\infty \frac{h}{2^2}=\frac{1/2}{(1-1/2)^2}\\\
=2.\\]


\\[O\left(n\sum\_{h=0}^{\lfloor lg n\rfloor}{\frac{h}{2^h}}\right)=O\left(n\sum\_{h=0}^{\infty}{\frac{h}{2^h}}\right)\\\
=O(n).\\]