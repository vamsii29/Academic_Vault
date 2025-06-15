---
layout : default
title: Chapter - 0 : Review of Concepts and Notations
---
<a id="Lektion-0"></a>
## Chapter - 0 : Review of Concepts and Notations
---
### 0.1-Logs-and-Exponents:
<a id="0.1-Logs-and-Exponents"></a>
Some basic Stuff of Logs and exponents
1. $(x^a)(x^b) = (x)^{a+b}$
2. $(x^a)^b = (x)^{ab}$
3. $\log_x(ab) = \log_x(a) + \log_x(b)$
4. $a \log_xb = \log_x(b^a)$

### 0.2-Modular-Arithmetic
<a id="0.2-Modular-Arithmetic"></a>
Some basic stuff to recap
	1. We write set of integers as: 
		$\mathbb{Z} \overset{\text{def}}{=} \{ \ldots, -2, -1, 0, 1, 2, \ldots \}$
	2. We write set of Natural numbers as 
		$\mathbb{N} \overset{\text{def}}{=} \{0, 1, 2, 3, \ldots \}$

**1. Definition** : for $x, n \in \mathbb{Z}$ , we say that $n$ **divides** $x$ (or $x$ is a **multiple** of $n$ ), and write $n \mid x$ , if there exists an integer $k$ such that $x = kn$. 
**2. Definition** : Let $n$ be a positive integer, and let $a$ be any integer. The expression $a$ % $n$ (usually read as $a \bmod n$ )  represents the remainder after dividing $a$ by $n$. More formally, $a$ % $n$ is the unique $r \in {{0 ,\ldots, n-1}}$ such that $n \mid (a-r)$. 
	Pay attention that '$a\mod n$' is always a non negative number, even if $a$ is negative.
	example: 
		21 mod 7 = 0 because 21 = 3 . 7 + <u>0</u>
		-20 mod 7 = 1 because -20 = (-3) . 7 + <u>1</u> 
		-1 mod 7 = 6 because -1 = (-1) . 7 + <u>6</u>
**3. Definition** : For positive $n$, we write $\mathbb{Z}_n \overset{\text{def}}{=} \{0, 1, 2, \ldots, n-1\}$ to denote the set of integers modulo $n$. These are the possible remainders one obtains by dividing by $n^2$.  
**4. Definition** : For positive $n$, we say that integers $a$ and $b$ are **congruent modulo** $n$, and write $a \equiv_n b \iff a \bmod n = b \bmod n$
	 1. $a \equiv_n b$ : In this expression, $a$ and $b$ can be integers of any size, and any sign. The left and right side have a certain relationship modulo $n$.
	2. $a = b \bmod n$ : This expression says that two integers are equal. The '=' rather than '$\equiv$' is the clue that the expression refers to equailty over the integers. "$b \bmod n$" on the right-hand side is an operation performed on two integers that returns an integer results. The result of  $b \bmod n$ is an integer in the range $\{0, 1, 2, \ldots, n-1 \}$.
	example: "99 $\equiv_{10}$ 19" is true. Applying the deifintion. we see that 10 divides 99 - 19.
		    on the other hand, " 99 = 19 % 10 " is *false* the right - hand side evaluated to the integer 9, but 99 and 9 are different integers.
	 In short the expression like $a \equiv_n b$ make sense for any $a, b$ (including negitive!), but expressions like $a = b$ % $n$ make sense only if $a \in \mathbb{Z_n}$.

 If $d \mid x$ and $d \mid y$, then $d$ is a **common divisor** of $x$ and $y$. the largest possible such $d$ is called the **greatest common divisor (GCD)**, denoted gcd($x , y$). if gcd($x ,y$) = 1, then we say that $x$ and $y$ are **relatively prime**.


**Tips and Tricks:**

Example: we can evaluate the expression 6 . 7 . 8 . 9 . 10 % 11 without ever calculating that product over the integers, by using the following reasoning:
	$$
	6 . 7 . 8 . 9 . 10 = (42) . 8 . 9 . 10
	$$
	$$\equiv_{11} 9 . 8 . 9 . 10 $$
	$$= (72) . 9 . 10$$
	$$\equiv_{11} 6 . 9 . 10$$
	$$= (54) . 10$$
	$$\equiv_{11} 10 . 10$$
	$$= 100$$
	$$\equiv_{11} 1$$

### 0.3-Strings
<a id="0.3-Strings"></a>

**Definition** : when $x$ and $y$ are strings of the same length, we write $x \oplus y$ to denote the bitwise exclusive-or (XOR) of the two strings. The expression $x \oplus y$ is generally not defined when the strings are different lengths, but in rare occasions it is useful to consider the shorter string being padded with 0s. When that's the case, we must have an explicit convention about whether the shorter string is padded with leading 0s or trailing 0s. 
	 Example:  0011 $\oplus$ 0101 = 0110. The following facts about the XOR operation are frequently useful:
		-  $x \oplus x = 000...$                   XOR'ing a string with itself results in zeroes.
		- $x \oplus 000...$ = $x$                     XOR'ing with zeros has no effect.
		- $x \oplus 111... = \overline{x}$                    XOR'ing with ones flips every bit. 
		- $x \oplus y = y \oplus x$                     XOR is symmetric.
		- $(x \oplus y) \oplus z = x \oplus (y \oplus z)$  XOR is associative.
		- 
 **Bit-flipping** : Note that XOR'ing a bit with 0 has no effect, while XOR'ing with 1 flips that bit.
 **Addition mod-2** : XOR is just addition mod 2 in every bit. This way of thinking about XOR helps to explain why "algebraic" things like $(x \oplus y) \oplus z = x \oplus (y \oplus z)$ are true. They are true for addition so they are true for XOR.
 **Definition** : we write $x \parallel y$  to denote the result of concatenating $x$ and $y$.

### 0.4-Functions
<a id="0.4-Functions"></a>

Let $X$ and $Y$ be finite sets. A function $f : X \rightarrow Y$ is:
1. **Injective** : (1-to-1) if it maps distinct inputs to distinct outputs. Formally: $x \ne x' \Rightarrow f(x) \ne f(x')$. If there is an injective function from $X$ to $Y$, then we must have $|Y| \ge |X|$.
2. **Surjective** : (onto) if every element in $Y$ is a possible output of $f$. Formally: for all $y \in Y$ there exists an $x \in X$ with $f(x) = y$. if there is a surjective function from $X$ to $Y$, then we must have $|Y| \le |X|$.
3. **Bijective** : (1-to-1 correspondence) if $f$ is both **injective and surjective**. If there is a bijective function from $X$ to $Y$, then we must have $|X| = |Y|$.

### 0.5-Probability
<a id="0.5-Probability"></a>

**Definition** : A (*discrete*) probability distribution over a set $X$ of outcomes is usually written as a function "$\Pr$" that associates each outcome $x \in X$ with a probability $\Pr[x]$. We often say that the distribution assigns probability $\Pr[x]$ to outcome $x$.
	- for each outcome $x \in X$, the probability distribution must satisfy the condition $0 \le \Pr[x] \le 1$. Additionally, the sum of all probabilities $\sum_{x \in X} \Pr[x]$ must equal 1.
**Definition** : A special distribution is the uniform distribution over a finite set $X$, in which every $x \in X$ is assigned probability $\Pr[x] = \frac{1}{|X|}$. 
	- We also extend the notation $\Pr$ to events, which are collections of outcomes. Formally , an event $A$ is any subset of the possible outcomes, and its probability is defined to be $\Pr[A] = \sum_{x \in A} \Pr[x]$. we always simplify the notation slightly, so instead of writing $\Pr[\{x \mid x \ \text{satisifies some condition}\}]$, we write $\Pr[condition]$.


**Tips and Tricks:**

 1. Knowing one of the probabilities $\Pr[A]$ and $\Pr[\neg A]$ (which is "the probability that $A$ doesn't happen") tells us exactly waht the other probability is, via the relationship
		$$
		\Pr[A] = 1 - \Pr[\neg A]
		$$
2.  This is one of the most basic facts about probability, but it can be surprisingly useful since one of $\Pr[A]$ and $\Pr[\neg A]$ is often much easier to calculate than the other.

#### Using Precise terminology 

- saying "$x$ is a random string" is sloppy language.
- Randomness is a property of the process, not the outcome.
- Prefer saying:  "$x$ was choosen randomly"
- Even better: "$x$ was choosen uniformly (from a set)", if thats the intended meaning
- in cryptography, people often use "random" to mean "uniformly random", but clarity helps avoid confusion
- key habit: Be precise - randomness comes from how a value is selected, not 

### 0.6-Notations-in-Pseudocode
<a id="0.6-Notations-in-Pseudocode"></a>

We'll often describe algorithm / process using pseudocode.
1. $\leftarrow$
	- When $D$ is a probability distribution, we write $x \leftarrow D$ to mean "sample $x$ according to the distribution $D$."
	- If $A$ is an algorithm that takes input and also makes some internal random choices, then it is natural to think of its output $A(y)$ as a distribution - possibly a different distribution for each input $y$. Then we write $x \leftarrow A(y)$ to mean the natural thing: "run $A$ on input $y$ and assign the output to $x$." 
	- We overload the "$\leftarrow$" notation slightly, writing "$x \leftarrow X$" when $X$ is a finite set to mean that $x$ is sampled from the *uniform distribution* over $X$.

2. $\coloneqq$
	- We write $x \coloneqq y$ for the assignments to variables: "take the value of expression $y$ and assign it to variable $x$. "
3. $\stackrel{?}{=}$ 
	- We write comparisons as $\stackrel{?}{=}$ (analogous to "$==$ in C programming language"). So $x \stackrel{?}{=} y$ doesn't modify $x$ (or $y$), but rather it is an expression which returns $\text{true}$ if $x$ and $y$ are equal.
	- it is often seen in the conditional part of an if-statement, but also in return statements as well.

	### **Subroutine Conventions**
	- We'll use mathematical notations to define the types of subroutine arguments:
		$$
		\frac{\texttt{FOO} (x \in \{0,1\}^*):}{\quad \ldots}
		$$
		means
		$$\texttt{void} \quad \texttt{foo(string\:x)} \quad  \{ \ldots \}$$

### 0.7-Asymptotic-Notations
<a id="0.7-Asymptotic-Notatio"></a>

Let $f : \mathbb{N} \rightarrow \mathbb{N}$ be a function. We characterize the asymptotic growth of $f$ in the following ways"

- #### Big - O Notation:  

	$f(n)$ is $O(g(n))$  $\overset{\text{def}}{\Longleftrightarrow}$  $\displaystyle \lim_{n \to \infty} \frac{f(n)}{g(n)} < \infty$  
                $\iff$ $\exists c > 0 :$ for all but finitely many $n$ : $f(n) < c \cdot g(n)$


- #### Big - Omega Notation:

	$f(n)$ is $\Omega(g(n))$  $\overset{\text{def}}{\Longleftrightarrow}$  $\displaystyle \lim_{n \to \infty} \frac{f(n)}{g(n)} > 0$  
                $\iff$ $\exists c > 0 :$ for all but finitely many $n$ : $f(n) > c \cdot g(n)$

- #### Big - Theta Notation:

	$f(n)$ is $\Theta(g(n))$  $\overset{\text{def}}{\Longleftrightarrow}$  $f(n)$ is $O(g(n))$ and $\Omega(g(n))$  
                $\iff$ $0 < \displaystyle \lim_{n \to \infty} \frac{f(n)}{g(n)} < \infty$  
                $\iff$ $\exists c_1, c_2 > 0$ : for all but finitely many $n$ : 
                             $c_1 \cdot g(n) < f(n) < c_2 \cdot g(n)$


---
