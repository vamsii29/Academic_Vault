
This cheatsheet covers the most common LaTeX symbols and structures that work in Obsidian using MathJax.

---

## 🔢 Basic Math

| Description        | Syntax              | Output         |
|--------------------|---------------------|----------------|
| Inline math        | `$x + y$`           | $x + y$        |
| Display block      | `$$x + y$$`         | $$x + y$$      |
| Superscript        | `x^2`               | $x^2$          |
| Subscript          | `a_1`               | $a_1$          |
| Fractions          | `\frac{a}{b}`       | $\frac{a}{b}$  |
| Roots              | `\sqrt{2}`, `\sqrt[3]{x}` | $\sqrt{2}$, $\sqrt[3]{x}$ |
| Parentheses        | `\left( x \right)`  | $\left( x \right)$ |

---

## 🔠 Greek Letters

| Name        | Lowercase     | Uppercase     |
|-------------|---------------|---------------|
| Alpha       | `\alpha` → $\alpha$ | `\Alpha` *(not standard)* |
| Beta        | `\beta` → $\beta$ | —             |
| Gamma       | `\gamma` → $\gamma$ | `\Gamma` → $\Gamma$ |
| Delta       | `\delta` → $\delta$ | `\Delta` → $\Delta$ |
| Pi          | `\pi` → $\pi$ | `\Pi` → $\Pi$ |

---

## 🧮 Logic and Sets

| Description              | Syntax                  | Output               |
|--------------------------|-------------------------|----------------------|
| Element of               | `\in`                   | $x \in A$            |
| Not in                   | `\notin`                | $x \notin A$         |
| Subset                   | `\subseteq`             | $A \subseteq B$      |
| Union / Intersection     | `\cup`, `\cap`          | $A \cup B$, $A \cap B$ |
| Set                      | `\{x \mid x > 0\}`      | $\{x \mid x > 0\}$   |
| Natural numbers          | `\mathbb{N}`            | $\mathbb{N}$         |
| Integers                 | `\mathbb{Z}`            | $\mathbb{Z}$         |

---

## 🔄 Modular Arithmetic

| Description          | Syntax                    | Output                |
|----------------------|---------------------------|------------------------|
| Mod operator         | `a \bmod n`               | $a \bmod n$           |
| Divides              | `a \mid b`                | $a \mid b$            |
| Does not divide      | `a \nmid b`               | $a \nmid b$           |
| Congruence           | `a \equiv b \pmod{n}`     | $a \equiv b \pmod{n}$ |
| Z mod n              | `\mathbb{Z}_n`            | $\mathbb{Z}_n$        |

---

## 📐 Comparison and Logic

| Description        | Syntax            | Output           |
|--------------------|-------------------|------------------|
| Equals             | `=`               | $a = b$          |
| Not equal          | `\ne`             | $a \ne b$        |
| Less / Greater     | `<`, `>`          | $a < b$          |
| Less than or equal | `\le`             | $a \le b$        |
| And / Or           | `\land`, `\lor`   | $A \land B$, $A \lor B$ |
| Not                | `\neg`            | $\neg A$         |
| Implies / IFF      | `\Rightarrow`, `\iff` | $A \Rightarrow B$, $A \iff B$ |

---

## 💡 Probability and Logic

| Description                    | Syntax                         | Output                    |
|--------------------------------|--------------------------------|---------------------------|
| Probability                    | `\Pr[A]`                       | $\Pr[A]$                  |
| Expectation                    | `\mathbb{E}[X]`                | $\mathbb{E}[X]$           |
| Sampling                       | `x \leftarrow D`               | $x \leftarrow D$          |
| Randomized output              | `x \leftarrow \mathcal{A}(y)` | $x \leftarrow \mathcal{A}(y)$ |
| True / False (text)            | `\text{true}` / `\text{false}` | $\text{true}$             |
| Comparison (like `==`)         | `x \stackrel{?}{=} y`          | $x \stackrel{?}{=} y$     |

---

## ⏱️ Asymptotic Notation

| Description     | Syntax                              | Output                      |
|-----------------|-------------------------------------|-----------------------------|
| Big-O           | `O(g(n))`                           | $O(g(n))$                   |
| Big-Omega       | `\Omega(g(n))`                      | $\Omega(g(n))$              |
| Big-Theta       | `\Theta(g(n))`                      | $\Theta(g(n))$              |
| Limit           | `\lim_{n \to \infty}`               | $\lim_{n \to \infty}$       |
| Full example    | `\lim_{n \to \infty} \frac{f(n)}{g(n)} < \infty` | $\lim_{n \to \infty} \frac{f(n)}{g(n)} < \infty$ |

---

## ✍️ Formatting and Spacing

| Description          | Syntax          | Output          |
|----------------------|-----------------|-----------------|
| Text in math         | `\text{word}`   | $\text{word}$   |
| Line break           | `\\`            |                 |
| Small space          | `\,`            | $a\,b$          |
| Medium space         | `\:`            | $a\:b$          |
| Large space          | `\;`            | $a\;b$          |
| Quad space           | `\quad`         | $a\quad b$      |

---

## 🧠 Extras

- Use `\left(...\right)` to auto-size parentheses:  
  `$ \left( \frac{a}{b} \right) $`
- Use `\overset{?}{=}` or `\stackrel{?}{=}` for equality tests.
- Use `\ldots`, `\cdots` for ellipsis:  
  `$a_1, a_2, \ldots, a_n$`

---