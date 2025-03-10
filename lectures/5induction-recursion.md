---
marp: true
paginate: true
size: 16:10
theme: default
class: invert
---

### Examples for basic structures

```math
A = \begin{bmatrix}
1&0&0&1\\
0&1&0&1\\
1&1&1&1
\end{bmatrix}, 
B = \begin{bmatrix}
1&0\\
0&1\\
1&0
\end{bmatrix}
```
- Find $A \lor B$
- Find the Boolean product for $A$ and $B$: $A \odot B$
- Find $A^{[2]}$, the 2nd Boolean product of $A$

---

# Induction and recursion
Slides are based on
[Notes by James Aspnes](https://www.cs.yale.edu/homes/aspnes/classes/202/notes.pdf)

---  

**Induction** is a technique for proving universal statements about some class of objects built from smaller objects: 
- the idea is to show that if each object has a property provided all the smaller objects do, then every object in the class has the property.

---

**Recursion** is the same technique applied to
definitions instead of proofs: 
- an object is defined in terms of smaller objects of the same type.

---

## Simple Induction

- we use this to show that something is true for all natural numbers.

- Most definitions of the natural numbers $\mathtt{N}$ has  the following basic pattern

 - 0 is a natural number.
- If $x$ is a natural number, so is $x + 1$.


This is **an example of a recursive definition!**

--- 

## Induction schema

```math
(P(0) \land \forall x \in N : (P (x) \to P (x + 1))) \to \forall x \in N : P(x).
```

This means showing that $P(0)$ is true and that $P(x)$ implies $P(x + 1)$.

- **The proof with the induction schema**:
1. **the base case:** show that P(0) holds,
2. **the induction step:** show that
$P(x) \to P(x + 1)$. 
- **the induction hypothesis:** assume $P(x)$ holds
- then show that with this assumption, $P(x+1)$ holds
 
---  
**Example:**
show that for all $n \in N$, either
$n = 0$ or there exists $n'$ such that $n = n' + 1$.

---

**Proof:**
Let P(n) be $x = 0 \lor (\exists x': x = x' + 1)$  
We are trying to show that P(n) holds for all n.


- **Base case:** $n=0.$ 
- **Induction step:**
    - **Induction hypothesis:** $P(x)$ holds.
    - $P(x+1)$ is $x+1 = 0 \lor (\exists x' : x+1 = x' + 1)$
    -  for $x'=x$ the hypothesis holds.
 
---  

**Example:**
```math
x^0 = 1,\\ 
x^{n+1} = x\cdot x^n.
```

This is a recursive definition: 
```math
2^4 = 2\cdot 2^3 = 2\cdot2\cdot 2^2 = 2\cdot2\cdot 2\cdot 2^1 =2\cdot2\cdot2\cdot2\cdot 2^0 = 2\cdot2\cdot2\cdot2\cdot 1 = 16
```

---  

**Example:**
If $a>1$, then $a^n>1$ for all $n>0$.

---

**Proof:**
- **Base case:** if $n=0$, then $n\ngeq 0$.
- **Inductive step:** Suppose it holds for $n$. For $n+1$, we have two cases:
    - if $n=0$, then $a^1 =a\cdot a^0 = a > 1$
    - if $n>0$, then $a^{n+1} = a\cdot a^n > a\cdot 1 > 1$ 

---  

### Alternative base case:
Generalized version of induction schema:
```math
(P (z_0 ) \land \forall z \in Z, z \geq z_0 : (P (z) \to P (z + 1))) \to \forall z \in Z, z \geq z_0 : P (z)
```
- if P is true for $z_0$,  then any larger integer can be reached by applying +1 enough times, and each +1 operation preserves P.

---  

**Example:**
Let $n \in N$. If $n\geq 4$, then $2^n \geq n^2.$

---

**Proof:**

- **Base case:** For n=4, $2^4 = 16 = 4^2.$
- **Induction step:**
    - Assume $2^n \geq n^2.$
    - Show that $2^{n+1} \geq (n+1)^2 = n^2 + 2n + 1.$
```math
2^{n+1} =  2 \times 2^n \geq  2n^2
```
```math
2n^2 = n^2+n^2 \geq  n^2 + 4n
```
note that when $n \geq 4; n^2 \geq 4n$:
```math
n^2 + 4n =  n^2 +2n+2n \geq n^2 +2n +1=(n+1)^2.
```

---

### Recursive definitions work

**lemma**
Let $S$ be some codomain, let $g : S \to S$, and let $f (n) : N \to S$
satisfy
```math
f(0) =  x_0
```
```math
f(n+1) =  g(f(n))
```
Then there is a function $f$ with this property.

---

**Proof:**
Suppose that there is some $f'$ such that $f'(0) = x_0$ and $f'(n + 1) =
g(f'(n))$.

- base case:$f'(0) = x_0 = f(0)$
- induction step: If $f'(n) = f(n)$, then $f'(n+1) = g(f'(n)) = g(f(n)) = f(n+1).$   

---

### A diferent way to think induction
In set-theoretic terms, the principle of induction says that if S is a subset of N, and both
- $0\in S$ and
- $x\in S$ implies $x+1 \in S$,
then $S= N$.

---

## Strong Induction

When proving for $n + 1$
- use the fact that the induction hypothesis  holds for all $n' < n + 1$, not just for $n$.

Instead of original
```math
\forall k : P (k) \to P (k +1),
```

we prove strong induction:
```math
\forall k : (\forall m \leq k : Q(m)) \to Q(k + 1).
```

---

## Recursively defined structures

A definition of a class of structures can often look like inductive proof, where we give a base case and a rule for building bigger structures from smaller ones.

**Example:** Complete binary trees 
- A complete binary tree consists of either 
    1. a leaf node,  
    2. or an internal node (the root) with two complete binary trees as children (or subtrees).

---

### Functions on recursive structures
**Factorial**: 
- Let `0! = 1`. 
- For `n > 0, let n! = n · ((n − 1)!)`.  

**The Fibonacci series** 
- Let `F(0) = F (1) = 1`. 
- For `n > 1`, let `F(n) = F(n − 1) + F(n − 2)`.

---

### Structural induction

- Recursively-defined objects and functions also lend themselves easily to
induction proofs

- **Structural induction** is used to prove that some proposition `P(x)` holds for all `x` of some sort of recursively defined structure, such as formulas, lists, or trees.

---  

**Example**
Binary tree with $n$ leaves has $n-1$ internal nodes

---

- **Base case:** a tree with 1 leaf
  - $n = 1$, $n-1 = 0$ leaf nodes
- **Induction step:** Let $n_1$ and $n_2$ be number of leaves in two subtrees.
  - $n_1+n_2 = n$. 
  - The number of internal nodes:
    - $(n_1-1)+(n_2-1) +1 (\text{the root})  = n-1$. 

---


**Example**
Show that a binary tree with depth $d$ has at most $2^{d+1} − 1$ nodes.

---

- **Base case:** a tree with 1 leaf
  - $d = 0$, $2^{0+1} − 1 = 1$ nodes
- **Induction step:** Given a tree of depth $d > 1$: it has 1 root node, two subtrees with at most depth $d-1$
  - nodes in one subtree $2^{d-1+1} − 1 = 2^d - 1$. 
  - The number of internal nodes:
    - $(2^d - 1)+(2^d - 1) +1  = 2^{d+1} - 1$. 

---



**Example:**
Consider the following recursively defined set $S$:

- $a \in S$
- If $x \in S$ , then $( x ) \in S$

Prove that every element of $S$ contains
an equal number of right and left parentheses.

---  

**Proof:**

- **Base case:** $a$ does not have parenthesis (0 ())
- **Inductive step:** x has $n$ number of right and left parentheses.

$(x)$ has $n + 1$ left and right parentheses, which is equal.

---

# Summation Notation

Given a sequence $x_a , x_{a+1} , . . . , x_b$ , $x_a + x_{a+1}+ . . .  +x_b$
is written as the **summation**:
```math
\sum_{i=a}^{b}x_i.
```

- The variable $i$ is  **the index of summation**
- $a$ is **the lower bound**
- $b$ is **the upper bound(or limit)**

---  

## Formal definition
We define the **summation** with the recurrence:
```math
\sum_{i=a}^{b}f(i)= \begin{cases} 0 & \text{if } b < a\\
f(a)+\sum_{i=a+1}^{b}f(i) &\text{otherwise}
\end{cases}.
```

---

**Example:**
```math
\sum_{i=1}^3i = 1+ \sum_{i=2}^3i= 1+2+ \sum_{i=3}^3i = 1+2+3+\sum_{i=4}^3i = 1+2+3+0=6.
```

---

**Example:**
```math
\sum_{i=1/2}^{9/4}i = 1/2+ \sum_{i=3/2}^{9/4}i = 1/2+ 3/2 +\sum_{i=5/2}^{9/4}i= 1/2+ 3/2 +0
```
---  

If $b-a$ is an integer, then
```math
\sum_{i=a}^{b}f(i)= 
\begin{cases}
&0 & \text{if } b < a\\
&f(b)+\sum_{i=a}^{b-1}f(i) &\text{otherwise}
\end{cases}.
```

---

**Proof:**

- For $b<a$, it is 0.
- For $b\geq a$, prove by induction:

- **Base case:** If $b-a = 0$, then 
```math
\sum_{i=a}^{b}f(i)= f(a) = f(b)=f(b)+\sum_{i=a}^{b-1}f(i).
```
---

- **Inductive step:** If $b-a> 0$, then 
```math
\sum_{i=a}^{b}f(i) = 
f(a)+\sum_{i=a+1}^{b}f(i)
= f(a)+f(b)+\sum_{i=a+1}^{b-1}f(i)=f(b)+\sum_{i=a}^{b-1}f(i). 
```

$b - (a + 1) = b - a - 1 < b - a$, so the middle step uses the inductive step.

---

### The scope:
```math
\sum_{i=1}^{n} i^2 +1 =\left(\sum_{i=1}^{n} i^2 \right)+1 
```

**The scope in addition:**
```math
\sum_{i=1}^{n} i^2 +\sum_{i=1}^{n} i =\left(\sum_{i=1}^{n} i^2 \right)+\left(\sum_{i=1}^{n} i \right) 
```

---

## Summation Identities
The summation is **linear**. That means:
```math
\sum_{i=n}^{m} ax_i  =a\sum_{i=n}^{m} x_i
```
and the sum can be split:
```math
\sum_{i=n}^{m} (x_i+y_i)  =\sum_{i=n}^{m} x_i + \sum_{i=n}^{m} y_i
```


---  

### Identities
The order can be changed:
```math
\sum_{i=n}^{m} \sum_{j=n'}^{m'} x_{ij} =\sum_{i=n'}^{m'} \sum_{j=n}^{m} x_{ij}
```
The product of sums:
```math
\left(\sum_{i=n}^{m} x_i\right)\left(\sum_{j=n'}^{m'} y_i\right)  =
\sum_{i=n}^{m} \sum_{j=n'}^{m'} x_iy_j
```

---


## Closed Forms

**Closed form:** Converting a summation into a simpler expression without any summation signs or other
operators that iterate over some bound variable. 
```math
\begin{align*}
& \sum_{i=1}^n 1 = n\\
& \sum_{i=1}^n i = \frac{n(n+1)}{2}\\
& \sum_{i=1}^n r^i = \frac{1-r^{n+1}}{1-r}\\
\end{align*}
```
Proofs are by induction.

---

### Guess but verify
$
S(n) = \sum_{k=1}^{n}(2k-1)
$

We write down a table of values:
```math
\begin{align*}
n && S(n)\\
0 & &0\\
1&&1\\
2 &&1+3=4\\
3 &&1+3+5=9\\
4 &&1+3+5+7=16\\
5 &&1+3+5+7=9=25\\
\end{align*}
```
**Guess:** $S(n) = n^2$. Verify it by induction... 

---
#### Ansatzes

Ansatz  is german-word for starting point.

Guess is made with parameters:

```math
\sum_{i=0}^{n}i^2 = c_3n^3 + c_2 n^2 + c_1 n + c_0, \text{ when }n \geq 0.
```

- If $n=0$, then  $\sum_{i=0}^{n}i^2 = 0 = c_0$.
- Plugging small n values, such as $n=1, n=2, n=3...$

---

```math
\begin{align*}
\text{for } n=1, & &0+1 = 1 = c_3+c_2+c_1\\
\text{for } n=2,& &0+1+4 = 5 = 8c_3+4c_2+ 2c_1\\
\text{for } n=3,& &0+1+4+9 = 14= 27c_3+8c_2+3c_1
\end{align*}
```
$\sum_{i=0}^{n}i^2 = \frac{1}{3}n^3+\frac{1}{2}n^2+\frac{1}{6}n$, then verify it with induction.

---

- **infinite sums:**
```math
\sum_{i=0}^{\infty} \frac{1}{i^2}.
```
- **Double sums:**
```math
a\times b {\stackrel{def}{=}} \sum_{i=1}^a\sum_{i=1}^b 1.
```
- **Products** ($\prod_{i=1}^a$):

- An empty product is 1.
```math
n! {\stackrel{def}{=}} \prod_{i=1}^n i = 1 \cdot 2 \cdot...\cdot n.
```

---

Other big operators

- Big AND:
```math
\bigwedge_{x\in S}^{} P(x) \equiv P (x_1 ) \land P (x_2 ) \land \dots 
\equiv \forall x \in S : P(x).
```
- Big OR:
```math
\bigvee_{x\in S}^{} P(x) \equiv P (x_1 ) \lor P (x_2 ) \lor \dots 
\equiv \exists x \in S : P(x).
```

---

- Big Intersection:
```math
\bigcap_{i=1}^{n} A_i = A_1\cap A_2 \cap \dots \cap A_n.
```
- Big Union:
```math
\bigcup_{i=1}^{n} A_i = A_1\cup A_2 \cup \dots \cup A_n.
```
