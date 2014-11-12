#32 String Matching

__*strings*__: character arrays.

We say that pattern $$$P$$$ __*occurs with shift s*__ in text $$$T$$$ (or, equivalently, that pattern $$$P$$$ __*occurs beginning at position s* + 1__ in text $$$T$$$) if $$$0 \leq s \leq n - m$$$ and $$$T[s + 1 .. s+ m] = P[1 ..m]$$$ (that is, if $$$T[s + j] = P[j]$$$, for $$$1 \leq j \leq m$$$). If $$$P$$$ occurs with shift $$$s$$$ in $$$T$$$, then we call $$$s$$$ a __*valid shift*__; otherwise, we call $$$s$$$ and __*invalid shift*__. The __*string-matching problem*__ is the problem of finding all valid shifts with which a given pattern $$$P$$$ occurs in a given text $$$T$$$.

###Notation and terminology

$$$\Sigma^*$$$ (read "sigma-star"): the set of all finite-length strings formed using characters from the alphabet $$$\Sigma$$$.

zero-length __*empty string*__: $$$\epsilon$$$, also belongs to $$$\Sigma^*$$$.

__*concatenation*__ of two strings $$$x$$$ and $$$y$$$, denoted $$$xy$$$, has length $$$|x| + |y|$$$, consisting the characters from x followed by the characters from y.

a string $$$w$$$ is a __*prefix*__ of a string $$$x$$$, denoted $$$w \sqsubset x$$$, if $$$x = wy$$$ for some string $$$y \in \Sigma^*$$$.

a string $$$w$$$ is a __*suffix*__ of a string $$$x$$$, denoted $$$w \sqsupset x$$$, if $$$x = yw$$$ for some string $$$y \in \Sigma^*$$$.

###*Lemma 32.1 (Overlapping-suffix lemma)*
Suppose that $$$x$$$, $$$y$$$, and $$$z$$$ are strings such that$$$x \sqsupset z$$$ and $$$y \sqsupset z$$$. If $$$|x| \leq |y|$$$, then $$$x \sqsupset y$$$. If $$$|x| \geq |y|$$$, then $$$y \sqsupset x$$$. If $$$|x| = |y|$$$, then $$$x = y$$$.

##32.1 The naive string-matching algorithm

	NAIVE-STRING-MATCHER(T, P)
		n = T.length
		m = P.length
		for s = 0 to n - m
			if P[1 .. m] == T[s + 1 .. s + m]
				print "Pattern occurs with shift s"
##32.2 The Rabin-Karp algorithm


$$$t_{s+1} = (d(t_s - T[s + 1]h) + T[s + m + 1])$$$ mod $$$q$$$.

	RABIN-KARP-MATCHER(T, P, d, q)
	1	n = T.length
	2	m = P.length
	3	h = d^(m - 1) mod q
	4	p = 0
	5	t_0 = 0
	6	for i = 1 to m	// preprocessing
	7		p = (dp + P[i]) mod q
	8		t_0 = (dt_0 + T[i]) mod q
	9	for s = 0 to n - m	// matching
	10		if p == t_s
	11			if P[1 .. m] == T[s + 1 .. s + m]
	12				print "Pattern occurs with shift" s
	13			if s < n - m
	14				t_s+1 = (d(t_s - T[s + 1]h) + T[s + m + 1]) mod q

The procedure RABIN-KARP-MATCHER works as follows. All characters are interpreted as radix-d digits. The subscripts on t are provided only for clarity; the program works correctly if all the subscripts are dropped. Line 3 initializes h to the value of the high-order digit position of an m-digit window. Lines 4–8 compute $$$p$$$ as the value of $$$P[1 .. m]$$$ mod $$$q$$$ and $$$t_0$$$ as the value of $$$T[1 .. m]$$$ mod $q$. The for loop of lines 9–14 iterates through all possible shifts s, maintaining the following invariant:
Whenever line 10 is executed, $$$t_s = T[s + 1 .. s + m]$$$ mod $$$q$$$.If $$$p = t_s$$$ in line 10 (a “hit”), then line 11 checks to see whether $$$P[1 … m] = T[s + 1 .. s + m]$$$ in order to rule out the possibility of a spurious hit. Line 12 prints out any valid shifts that are found. If s < n 􏰃 m (checked in line 13), then the for loop will execute at least one more time, and so line 14 first executes to ensure that the loop invariant holds when we get back to line 10. Line 14 computes the value of $$$t_{s+1}$$$ mod $$$q$$$ from the value of $$$t_s$$$ mod $$$q$$$ in constant time using equation (32.2) directly.
##32.3 String matching with finite automata
###Finite Automata
A __*finite automaton*__ M, is a 5-tuple $$$(Q, q_0, A, \Sigma, \delta)$$$, where
*	$$$Q$$$ is a finite set of __*states*__,*	$$$q_0 \in Q$$$ is the __*start state*__,*	$$$ A \subseteq Q$$$ is a distinguished set of __#accepting states*__,* 	$$$\Sigma$$$ is a finite __*input alphabet*__,*	$$$\delta$$$ is a function from $$$Q \times \Sigma$$$ into $$$Q$$$, called the __*transition function*__ of $$$M$$$.


---
__*final-state function*__: $$$\phi(w): \Sigma^* \rightarrow Q$$$

$$$\phi(\epsilon) = q_0$$$

$$$\phi(wa) = \delta(\phi(w), a)$$$ for $$$w \in \Sigma^*, a \in \Sigma$$$

###String-matching automata

__*suffix function*__: $$$\sigma(x): \Sigma^* \rightarrow \\{0, 1, …, m\\}(Q)$$$

$$$\sigma(x) = max \\{k: P_k \sqsupset x\\}$$$

---
We define the string-matching automaton that corresponds to a given pattern $$$P[1 .. m]$$$ as follows:

*	The state set $$$Q$$$ is $$$\\{0, 1, …, m\\}$$$. The start state $$$q_0$$$ is state 0, and state $$$m$$$ is the only accepting state.
*	The transition function $$$\delta$$$ is defined by the following equation, for any state $$$q$$$ and character $$$a$$$:
	$$$\delta(q, a) = \sigma(P_qa)$$$.

$$$\phi(T_i) = \sigma(T_i)$$$

	FINITE-AUTOMATION-MATCHER(T, \delta, m)
	1	n = T.length
	2	q = 0
	3	for i = 1 to n
	4		q = \delta(q, T[i])
	5		if q == m
	6			print "Pattern occurs with shift" i - m

###*Lemma 32.2 (Suffix-function inequality)*
For any string $$$x$$$ and character $$$a$$$, we have $$$\sigma(xa) \leq \sigma(x) + 1$$$.

###*Lemma 32.3 (Suffix-function recursion lemma)*
For any string $$$x$$$ and character $$$a$$$, if $$$q = \sigma(x)$$$, then $$$\sigma(xa) = \sigma(P_qa)$$$.

###*Theorem 32.4*
If $$$\phi$$$ is the final-state function of a string-matching automaton for a given pattern $$$P$$$ and $$$T[1 .. n]$$$ is an input text for the automaton, then


$$$\phi(T_i) = \sigma(T_i)$$$

for $$$i = 0, 1, …, n$$$.

###Computing the transition function

	COMPUTE-TRANSITION-FUNCTION(P, \Sigma)
	1	m = P.length
	2	for q = 0 to m
	3		for each character a \in \Sigma
	4			k = min(m + 1, q + 2)
	5			repeat
	6				k = k - 1
	7			until P_k \sqsupset P_q a
	8			\delta(q, a) = k
	9	return \delta
	
