##15.4 Longest common subsequence

__Formalized notion__

Given a sequence \\(X = \<x_1, x_2, …, x_m\>\\), another sequence \\(Z = \<z_1, z_2, …, z_k\>\\) is a __*subsequence*__ of \\(X\\) such that for all \\(j = 1, 2, …, k\\), we have \\(x_{i_j} = z_j\\).

Given two sequences X and Y, we say that a sequence $$$Z$$$ is a __*command subsequence*__ of $$$X$$$ and $$$Y$$$ if $$$Z$$$ is a subsequence of both $$$X$$$ and $$$Y$$$.

In the __*longest-common-subsequence problem*__, we are given two sequences $$$X = <x_1, x_2, …, x_m>$$$ and $$$Y = <y_1, y_2, …, y_n>$$$ and wish to find a maximum-length common subsequence of $$$X$$$ and $$$Y$$$.

###Step 1: Characterizing a longest common subsequence

__*Therem 15. 1 (Optimal substructure of an LCS)*__

Let $$$X = <x_1, x_2, …, x_m>$$$ and $$$Y = <y_1, y_2, …, y_n>$$$ be sequences, and let $$$Z = <z_1, z_2, …, z_k>$$$ be any LCS of $$$X$$$ and $$$Y$$$.

1. If $$$x_m = y_n$$$, then $$$z_k = x_m = y_n$$$ and $$$Z\_{k-1}$$$ is an LCS of $$$X_{m - 1}$$$ and $$$Y\_{n-1}$$$.
2. If $$$x_m \neq y_n$$$, then $$$z_k \neq x_m$$$ implies that $$$Z$$$ is an LCS of $$$X_{m-1}$$$ and $$$Y$$$.
3. If $$$x_m \neq y_n$$$, then $$$z_k \neq y_n$$$ implies that $$$Z$$$ is an LCS of $$$X$$$ and $$$Y_{n-1}$$$.

###Step 2: A recursive solution

\\[c[i, j] = \begin{cases} 0&\text{if } i = 0 \text{ or }j = 0,\\\
c[i-1, j-1] + 1&\text{if }i, j > 0\text{ and } x_i = y_i,\\\
max(c[i, j-1], c[i-1, j])&\text{if }i, j > 0\text{ and } x_i \neq y_i.\end{cases}\\]

###Step 3: Computing the length of an LCS

	LCS-LENGTH(X, Y)
		m =  X.length
		n = Y.length
		let b[1 .. m, 	1 .. n] and c[0 .. m, 0 .. n] be new tables
		for i = 1 to m
			c[i, 0] = 0
		for j = 0 to n
			c[0, j] = 0
		for i = 1 to m
			for j = 1 to n
				if xi == yi
					c[i, j] = c[i - 1, j - 1] + 1
					b[i, j] = "\"
				elseif c[i - 1, j] >= c[i, j - 1]
					c[i, j] = c[i - 1, j]
					b[i, j] = "^"
				else c[i, j] = c[i, j - 1]
					b[i, j] = "<"
		return c and b
###Step 4: Constructing an LCS

	PRINT-LCS(b, X, i, j)
		if i == 0 or j == 0
			return
		if b[i, j] == "\"
			PRINT-LCS(b, X, i - 1, j - 1)
			print xi
		elseif b[i, j] == "^"
			PRINT-LCS(b, X, i - 1, j)
		else PRINT-LCS(b, X, i, j - 1)

			
###Improving the code


O(m + n) time


