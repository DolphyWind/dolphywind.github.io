---
title: 'Three Dimensional Numbers'
date: 2025-02-15T15:52:13+03:00
draft: false
toc: false
images:
tags:
  - algebra
  - math
author: "DolphyWind"
---

I was planning to write and publish this blogpost in late October 2024 but due to some relationship problems, mental health issues and emotional distress I delayed it for a bit.

If you have taken high school algebra class, I'm sure you are familiar with the [Complex Numbers](https://en.wikipedia.org/wiki/Complex_number). Those of you who dealt with 3D rotations before might've heard of 
[Quaternions](https://en.wikipedia.org/wiki/Quaternion), the 4D numbers. In this blogpost, we are going to aim for something in the middle, a number system with one real and two imaginary components,
I call these, the "Triplex numbers", with the form $a+bi+cj$ where $i$ and $j$ are the basis elements.

## First Steps
Complex numbers are defined by the identity $i^{2}=-1$, similary quaternions also have similar identities, precisely, $i^{2}=-1$, $j^{2}=-1$ and $k^{2}=-1$. Maybe, our numbers could be defined by $i^{2}=-1$
and $j^{2}=-1$. Let's investigate the product $ij$ and see if the math works out.
$$\text{Let } ij = a + bi + cj \hspace{1cm} \left(a,b,c \in \mathbb{R} \right)$$
$$\text{Left-multiply everything by }i$$
$$i^{2}j=ai+bi^{2}+cij$$
$$-j=ai-b+c(a+bi+cj)=ac-b + (cb+a)i + c^{2}j$$
Since this implies $c^{2}=-1$, and $c$ is a real number, there is no value of $c$ that satisfies this equation, thus a system with $i^{2}=-1$ and $j^{2}\=-1$ cannot exist.

We seem to have hit a huge road block, but don't worry, with a slight modification, we'll be able to define our number system. Instead of letting $i^{2}=-1$ and $j^{2}=-1$, we are going to let $i^{3}=-1$
and $j^{3}=-1$. Let's try to find what $i^{2}$ is equal to.
$$\text{Let } i^{2} = a + bi + cj$$
$$\text{Left-multiply everything by }i$$
$$i^{3} = ai + bi^{2} + cij$$
$$-1 = ai + b(a + bi + cj) + cij$$
$$-1 = ab + (a + b^{2})i + bcj + cij$$
We know that $(a+b^{2}) $ and $cb$ has to be equal to zero, since the latter involves multiplication of two real numbers, it is easier to investigate that. To make the product $cb$ to equal to zero; either $c$,
or $b$ has to be equal to zero. Choosing one gives two different number systems, in this blog post we'll investigate $b=0$ case.
$$-1 = ai+cij$$
And since the left hand side has $i$ terms, $a=0$. We're going to pick $c=-1$. These identities are enough to have a number system with the properties; 
$$i^3=j^3=-1$$
$$ij=ji=1$$
$$i^2=-j$$
$$j^2=-i$$

But this is not the only system that is consistent, there are more systems that are equally interesting for example;
$$\begin{align}
&i^3=j^3=ij=ji=1                &\hspace{1 cm}       &i^2=j   &\hspace{1 cm} &j^2=i    \hspace{1 cm} &\text{(Triplex numbers of the } 2^{\text{nd}} \text{ kind)} \\\\
&i^3=ij=ji=-1     \hspace{1 cm} &j^3=1 \hspace{1 cm} &i^2=j   &\hspace{1 cm} &j^2=-i   \hspace{1 cm} &\text{(Triplex numbers of the } 3^{\text{rd}} \text{ kind)} \\\\
&j^3=ij=ji=-1     \hspace{1 cm} &i^3=1 \hspace{1 cm} &i^2=-j  &\hspace{1 cm} &j^2=i    \hspace{1 cm} &\text{(Triplex numbers of the } 4^{\text{th}} \text{ kind)}
\end{align}$$

In fact, I first started studying triplex numbers of the $3^{rd}$ kind and then ported my work to this number system.


## Algebraic Operations
In this section, we'll define some operations on the triplex numbers. Mathematically speaking, for it to be a [ring](https://en.wikipedia.org/wiki/Ring_(mathematics)), only addition, subtraction and multiplication
suffices, but we'll also define division (as an inverse of multiplication). Subtraction will be implicitly defined as the inverse of addition. Since in a ring, additive inverses must exist.

Addition is simple and intuitive. If you have two numbers $x=a+bi+cj$ and $y=d+ei+fj$, then $x+y=(a + d) + (b + e)i + (c + f)j$.

Multiplication can be cumbersome to calculate, but it is just distributing multiplication over addition and combining like terms. Although, when it comes to the multiplication, there are some important
questions to ask: "Is multiplication, commutative?", "Do [zero divisors](https://en.wikipedia.org/wiki/Zero_divisor) exist?", "Do [units](https://en.wikipedia.org/wiki/Unit_(ring_theory)) exist?".

The answer to these three questions is yes. Showing commutativity is a trivial step, so I'll do what the best mathematicians do and leave it to you as an exercise.

To show the existence of units, you
can pick a number like $5+0i+0j$ and observe that $\frac{1}{5} + 0i + 0j$ is its multiplicative inverse. You may try to find some zero divisors manually but in the following sections
we'll prove a theorem that is going to give us a way to determine whether given a triplex number is a zero divisor or not.

What about division? We can view the division operation as a two part process: Inversion and multiplication. Meaning, to calculate $\frac{a+bi+cj}{d+ei+fj}$, we can first find
$\frac{1}{d+ei+fj}$ and multiply that with $a+bi+cj$. In complex numbers and quaternions, we can find the multiplicative inverse via the help of the number's complex conjugate, which is
just the number you get after inverting the complex parts of the number. Will a similar approach help us here?
$$(a+bi+cj)(a-bi-cj)=(a^{2}-2bc)+c^{2}i+b^{2}j$$

Nope.

## The Division

Huh? Why did we get a whole new section for division? How hard could it-
$$\frac{1}{a+bi+cj}=\frac{(a^{2} - bc) - (c^{2}+ab)i - (b^{2}+ac)j}{a^{3}-b^{3}-c^{3}-3abc}$$
Epic.

While I think it is possible to algebraically solve for $d, e$ and $f$ in terms of $a, b$ and $c$ in the equation $(a+bi+cj)(d+ei+fj)=1$, I don't think it is possible to do that without going insane.
Instead, we're going to invent some new tools to aid us in the process. We're gonna get a bit mathy, so seat your belts.

#### Ring Homomorphisms & Isomorphisms
A ring homomorphism $\phi$ from ring $R$ to ring $S$ is a mapping from $R$ to $S$ that preserves the algebraic structure, that is, for $x, y \in R$, we have;
$$\phi(x + y) = \phi(x) + \phi(y)$$
$$\phi(xy)=\phi(x)\phi(y)$$

A ring isomorphism is a ring homomorphism that is bijective, meaning that we can invert it. Any two ring that is isomorphic to one another is algebraically equivalent, meaning that if one statement is true for one
it immediately implies that the same statement is true for the other. To show that two rings are isomorphic, we should first show that it indeed preserves the algebraic structure and then show that it is bijective.

#### Theorem 1: The Natural Matrix Isomorphism
The ring of triplex numbers $\mathbb{T}$ is isomorphic to the ring given below with operations matrix addition and matrix multiplication.
$$ M = \left\\{ \begin{bmatrix} a & b & c \\\\ c & a & -b \\\\ b & -c & a \end{bmatrix} \mid a, b, c \in \mathbb{R} \right\\} $$
with
$$\phi(a+bi+cj) = \begin{bmatrix} a & b & c \\\\ c & a & -b \\\\ b & -c & a \end{bmatrix} $$

**Proof:** It is pretty easy to see that $\phi(x+y) = \phi(x) + \phi(y)$, so let's show $\phi(xy)=\phi(x)\phi(y)$
$$\text{Let } x=a+bi+cj \text{ and } y=d+ei+fj $$
$$\begin{align}\phi(xy)=\phi\left[(a+bi+cj)(d+ei+fj)\right] =& \phi[(ad+bf+ce) + (ae+bd-cf)i + (af-be+cd)j]\\\\ =& \begin{bmatrix} (ad+bf+ce) & (ae+bd-cf) & (af-be+cd) \\\\ (af-be+cd) & (ad+bf+ce) & -(ae+bd-cf) \\\\ (ae+bd-cf) & -(af-be+cd) & (ad+bf+ce) \end{bmatrix}\end{align}$$
$$\phi(x)\phi(y) = \begin{bmatrix}a & b & c \\\\ c & a & -b \\\\ b & -c & a \end{bmatrix} \begin{bmatrix} d & e & f \\\\ f & d & -e \\\\ e & -f & d \end{bmatrix} = \begin{bmatrix} (ad+bf+ce) & (ae+bd-cf) & (af-be+cd) \\\\ (af-be+cd) & (ad+bf+ce) & -(ae+bd-cf) \\\\ (ae+bd-cf) & -(af-be+cd) & (ad+bf+ce) \end{bmatrix}$$

So $\phi$ preserves the algebraic structure. Notice that $\phi(x)=\phi(y)$ implies $x=y$ so it is injective and for any $\phi(x)=A$, there is only one value for $x$ so it is surjective. QED

#### Lemma 1: Inverse Of An Isomorphism Is An Isomorphism
Let $R$ and $S$ be rings. And let $\phi$ to be an isomorphism from ring $R$ to ring $S$. Then the inverse isomorphism $\phi^{-1}$ is an isomorphism from ring $S$ to ring $R$.

Proof is left as an exercise to the reader.

#### Lemma 2: Composition Of Two Isomorphisms Is An Isomorphism
Let $R$, $S$ and $T$ be rings. Let $\phi$ be an isomorphism from $R$ to $S$ and $\varphi$ be an isomorphism from $S$ to $T$. Then the composition of $\varphi \circ \phi$ is an isomorphism from $R$ to $T$.

Proof is left as an exercise to the reader.

### Actually Defining The Division
Now that we have our natural matrix isomorphism, we can use it to define division. Remember that we were trying to solve
$$(a+bi+cj)(d+ei+fj)=1$$
We can apply the natural matrix isomorphism $\phi$ to get.
$$\phi(a+bi+cj)\phi(d+ei+fj)=\phi(1)$$
$$\begin{bmatrix} a & b & c \\\\ c & a & -b \\\\ b & -c & a \end{bmatrix} \begin{bmatrix} d & e & f \\\\ f & d & -e \\\\ e & -f & d \end{bmatrix} = \begin{bmatrix} 1 & 0 & 0 \\\\ 0 & 1 & 0 \\\\ 0 & 0 & 1 \end{bmatrix}$$
We can multiply with the inverse of the first matrix, assuming its determinant, $a^{3} - b^{3} - c^{3} - 3abc$ is not zero.
$$ \begin{bmatrix} d & e & f \\\\ f & d & -e \\\\ e & -f & d \end{bmatrix} = \frac{1}{a^{3}-b^{3}-c^{3}-3abc} \begin{bmatrix}(a^{2} - bc) & -(c^{2} + ab) & -(b^{2} + ac) \\\\ -(b^{2} + ac) & (a^{2} - bc) & (c^{2} + ab) \\\\ -(c^2 + ab) & (b^{2} + ac) & (a^{2} - bc) \end{bmatrix}$$
Lastly, we apply $\phi^{-1}$ to both sides
$$d+ei+fj=\frac{(a^{2} - bc) - (c^{2} + ab)i - (b^{2} + ac)j}{a^{3} - b^{3} - c^{3} - 3abc}$$

For a triplex number $x=a+bi+cj$, the number $(a^{2}-bc) - (c^{2} + ab)i - (b^{2}+ac)j$ is important and will show up later, so from now on, I'll refer to it as the *multiplicative conjugate* of $x$.

## Zero Divisors
You may recall that I've talked about a theorem that is going to give us a way to find zero divisors. Now is time to prove that.
#### Theorem 2: The Zero Divisor Theorem
A non-zero triplex number $x \in \mathbb{T} $ is a zero divisor, if and only if $a^{3} - b^{3} - c^{3} - 3abc = 0$.

**Proof:** Since this is an if and only if statement, first, we'll prove it in one direction, and then prove it in the other.

Let $x$ to be a zero divisor, then there is a non-zero $y \in \mathbb{T}$, such that $yx=0$. Let $y=d+ei+fj$ and $x=a+bi+cj$. Then this means,
$$(d + ei + fj)(a + bi + cj)=0$$
$$ (da + ec + fb) + (db + ea - fc)i + (dc - eb + fa)j = 0 $$
This gives us three different equations to solve
$$ da + ec + fb = 0 $$
$$ db + ea - fc = 0 $$
$$ dc - eb + fa = 0 $$
Readers with a sharp eye would see that the above equation can be written as
$$ \begin{bmatrix} a & c & b \\\\ b & a & -c \\\\ c & -b & a \end{bmatrix} \begin{bmatrix} d \\\\ e \\\\ b \end{bmatrix} = \begin{bmatrix} 0 \\\\ 0 \\\\ 0 \end{bmatrix} $$
equivalently
$$ A \vec{\gamma} = \vec{0} $$

This equation holds true when $\vec{\gamma} = \vec{0} $ or $Det(A)=0$, since we said $b$ is a non-zero number, $\vec{\gamma}$ can't be the zero vector, hence the latter must be true.
$Det(A)=a^{3}-b^{3}-c^{3}-3abc=0$, this proves the first direction.

Now let's prove it in the other direction. 

Let $x=a+bi+cj$ be a non-zero triplex number, and let $a^3-b^3-c^3-3abc=0$. Let's multiply $x$ with its multiplicative conjugate.
$$ (a+bi+cj)\[(a^{2}-bc) - (c^{2} + ab)i - (b^{2} + ac)j \] = a^{3} - b^{3} - c^{3} - 3abc = 0 $$

If the multiplicative conjugate is non-zero, we are done. $x$ is a zero-divisor whenever $a^{3}-b^{3}-c^{3}-3abc = 0$. Let's see what happens when the multiplicative conjugate is zero. Setting it equal to zero
gives us three different equations.
$$\begin{aligned}
&a^{2} - bc = 0 \hspace{0.5cm} \to \hspace{0.5cm} a^{2} = +bc \\\\
&c^{2} + ab = 0 \hspace{0.5cm} \to \hspace{0.5cm} c^{2} = -ab \\\\
&b^{2} + ac = 0 \hspace{0.5cm} \to \hspace{0.5cm} b^{2} = -ac
\end{aligned}$$

Given that $x$ is non-zero, this means neither $a$, $b$ nor $c$ is zero, so we can freely divide those equations to each other to get
$$ \frac{a^{2}}{c^{2}} = \frac{bc}{-ab} \hspace{0.5cm} \to \hspace{0.5cm} a^{3}=-c^{3} $$
$$ \frac{a^{2}}{b^{2}} = \frac{bc}{-ac} \hspace{0.5cm} \to \hspace{0.5cm} a^{3}=-b^{3} $$

So the multiplicative conjugate is zero when $a^{3}=-b^{3}=-c^{3}$ or equivalently $a = -b = -c$. If we write everything in terms of $a$, $x$ becomes $a - ai - aj = a(1 -i -j)$. Notice that when multiplicative
conjugate is zero, the quantity $a^{3}-b^{3}-c^{3}-3abc$ is still zero. Anyway, to finish this proof, we only have to show that $1-i-j$ is a zero divisor. With some trial and error, we can see that it indeed is.
$$ (1-i-j)(1+i) = 1 + i - i + j - j - 1 = 0 $$
QED.

## Isomorphisms To Quotient Rings
In this section, we are going to find an isomorphism from the ring of triplex numbers to the rings like $\mathbb{R}[x] / \langle x^{3} + 1 \rangle$. Of course, before showing that statement is true, I have to explain what do
those symbols represent. We have some important ideas to cover, if you already know what ideals and quotient rings are don't be hesitant to skip ahead.

### Ideals
A (two-sided) ideal $I$ of ring $R$ is a [subring](https://en.wikipedia.org/wiki/Subring) where for every $r \in R$ and $a \in I$, both $ra$ and $ar$ is in $I$. Since ideals are subrings, they are closed under addition.
$\langle a \rangle$ denotes the ideal $\\{ra \mid r \in R\\}$ for a commutative ring $R$. Similarly, $rI$ denotes the ring $\\{ra \mid a \in I\\}$ and $r + I$ denotes $\\{r + a \mid a \in I\\}$ for some $r \in R$.

#### Lemma 3: If $a \in I$, then $a+I = I$
This is an important property of ideals. So it benefits us to prove it right now.

**Proof:** First, let's show $a+I \subseteq I$. Since $I$ is closed under addition, anything that is in $a+I$ is also in $I$. Hence, $a+I \subseteq I$.

Now let's show that $I \subseteq a+I$. Notice that any element $x \in I$ can be written as $(a + x) - a$. $a+x$ and $-a$ (inverse of $a + 0$) are both elements of $a+I$. Since $a + I$ is closed under addition, $x \in a + I$.
Hence $I \subseteq a+I$. Both $a+I \subseteq I$ and $I \subseteq a+I$ imply $a+I = I$.

### Quotient (Factor) Rings
Let $R$ be a ring and $I$ be a two-sided ideal of $R$. The set $R / I=\\{r + I \mid r \in R\\}$ forms a ring under the operations $(r_{1} + I) + (r_{2} + I) = (r_{1} + r_{2}) + I$ and $(r_{1}I)(r_{2}I)=(r_{1}r_{2}I)$.

Quotient rings extend the idea of remainders from modular arihmetic to arbitrary algebraic sturctures. For example consider the ring $\mathbb{Z}/\langle 5 \rangle = \\{0 + \langle 5 \rangle, 1 + \langle 5 \rangle,
2 + \langle 5 \rangle, 3 + \langle 5 \rangle, 4 + \langle 5 \rangle \\}$. This is essentially the integers modulo $5$ and the ideas from modular arithmetic have direct, corresponding meanings. For example $0 \equiv 5 \pmod{5}$
means the sets $0 + \langle 5 \rangle$ and $5 + \langle 5 \rangle$ are the same sets. Of course with quotient rings we extend those ideas to any arbitrary mathematical object as long as they meet some criteria.

### Polynomial Rings
Let $R$ be a commutative ring. $R[x]$ denotes the ring $\\{a_{0} + a_{1}x + \dots + a_{n}x^{n}\\}$, where $a_{0}, a_{1}, \dots, a_{n} \in R$. In plain English, that is the ring of polynomials whose coefficients are from the
ring $R$.

### Defining The Isomorphisms
#### Theorem 3: Isomorphism 1
The set of triplex numbers $\mathbb{T}$ is isomorphic to the ring $\mathbb{R}[X]/\langle x^3 + 1 \rangle$.

Before attempting to prove the statement above, we first have to understand the shape of the elements of $\mathbb{R}[X]/\langle x^{3} + 1 \rangle$. For any arbitrary element of shape $p(x) + \langle x^{3} + 1 \rangle$, where
$p(x)$ is a polynomial with coefficients from $\mathbb{R}$, we can rewrite $p(x)$ as $(x^3 + 1)q(x)+r(x)$ where $deg[r(x)] \leq 2$ by using simple polynomial division. And since the term $q(x)(x^3+1) \in \langle x^{3} + 1 \rangle$,
it is absorbed and $p(x) + \langle x^{3} + 1 \rangle = r(x) + \langle x^{3} + 1 \rangle$, meaning that any element of $R[X]/\langle x^{3} + 1 \rangle$ has the shape $(a+bx+cx^{2}) + \langle x^{3} + 1 \rangle$.

To find what higher degree elements e.g. $x^{4} + \langle x^{3} + 1 \rangle$ equal to, we can use a neat trick. Since $x^{3} + 1 \in \langle x^{3} + 1\rangle$, we know that $x^3+1 + \langle x^3+1\rangle$ is equalt to the set
$0 + \langle x^{3} + 1\rangle$. Therefore, we can treat $x^{3} + 1$ as if it were equal to $0$ and replace $x^{3}$ with $-1$.

To prove the theorem, I'll give two proofs, one will be given by directly defining the isomorphism and showing it preserves the algebraic structure, and the other will be proven using something called the 
[The First Isomorphism Theorem](https://en.wikipedia.org/wiki/Isomorphism_theorems#Theorem_A_(rings)).

**Proof 3.1:** Let's define a mapping $\phi$ from $\mathbb{T}$ to $\mathbb{R}[X]/\langle x^{3} + 1 \rangle$ via the mapping $a+bi+cj \mapsto (a+bx-cx^{2} + \langle x^{3} + 1 \rangle)$. For brevity, I'll omit writing 
$\langle x^{3} + 1 \rangle$ every single time.

Notice that this mapping is already bijective. Let's check its structure preserving properties. It is trivial to see that $\phi(x + y) = \phi(x) + \phi(y)$ so let $x=a+bi+cj$ and $y=d+ei+fj$ to show $\phi(xy)=\phi(x)\phi(y)$.
$$\phi(x)\phi(y) = (a + bx - cx^{2})(d + ex - fx^{2}) = (ad + bf + ce) + (ae + bd - cf)x - (af - be + cd)x^{2}$$
$$\begin{align}\phi(xy) = \phi\left\[ (a+bi+cj)(d+ei+fj) \right\] &= \phi\left\[ (ad + bf + ce) + (ae + bd - cf)i + (af - be + cd)j \right\]\\\\ &= (ad + bf + ce) + (ae + bd - cf)x - (af - be + cd)x^{2}\end{align}$$

QED.

**Proof 3.2:** Let's define a homomorphism $\phi: \mathbb{R}[X] \to \mathbb{T}$ by the mapping $p(x) \mapsto p(i)$ and find kernel of this homomorphism, which is the ring of elements that map to $0$ in $\mathbb{T}$.
Since $i^{3} = -1$, the kernel is the set of all polynomials with $(x^{3} + 1)$ as a factor, which is the set $\langle x^{3} + 1 \rangle$. By the first isomorphism theorem, we how that there exist an isomorphism $\varphi$
from $R[X]/\langle x^{3} + 1 \rangle $ to $ \mathbb{T}$. Since $\varphi^{-1}$ itself is an isomorphism, $\mathbb{T} \approx R[X]/\langle x^{3} + 1 \rangle$. QED.

#### Theorem 4: Isomorphism 2
The ring of triplex numbers $\mathbb{T}$ is isomorphic to the ring $\mathbb{R}[X]/\langle x^{3} - 1 \rangle$.

**Proof:** This theorem can be proven using the first isomorphism theorem, similar to the Proof 3.2. Define a homomorphism $\phi: \mathbb{R}[X] \to \mathbb{T}$ with the mapping $p(x) \mapsto p(-i)$. The kernel of this homomorphism
is the set $\langle x^{3} - 1 \rangle$. And by the first isomorphism theorem, we have that $\mathbb{T} \approx R[X]/\langle x^{3} - 1 \rangle$. QED.

#### Theorem 5 
The set $\mathbb{R}[X]/\langle x^{3} + 1\rangle$ and $\mathbb{R}[X]/\langle x^{3} - 1 \rangle$ are isomorphic to eachother.

**Proof:** This is a direct consequence of [Theorem 3](#theorem-3-isomorphism-1) and [Theorem 4](#theorem-4-isomorphism-2). $R[X]/\langle x^{3} - 1 \rangle \approx \mathbb{T}$ and $\mathbb{T} \approx R[X]/\langle x^{3} + 1 \rangle$ imply $R[X]/\langle x^{3} - 1 \rangle \approx
R[X]/\langle x^{3} + 1 \rangle$ since composition of two isomorphisms is itself an isomorphism.

### End Of This Section
In this section we've investigated the underlying algebraic structure of the triplex numbers and we even found a new way to prove $R[X]/\langle x^{3} + 1\rangle \approx R[X]/\langle x^{3} - 1\rangle$. In the next section,
we're gonna explore the other kinds of triplex numbers and finish this post.

## Isomorphisms Between Other Kinds of Triplex Numbers
As you may recall, I also talked about other kinds of triplex numbers. In this section we are going to find isomorphisms between those kinds of triplex numbers. I'll use the subscript notation to refer to different
kinds of triplex numbers. Meaning $\mathbb{T_{n}}$ will refer to the triplex numbers of the $n^{\text{th}}$ kind.

The isomorphism between $\mathbb{T_{3}}$ and $\mathbb{T_{4}}$ is really easy to see. It is the mapping $a+bi_{3}+cj_{3} \mapsto a+ci_{4}+bj_{4}$.
#### Theorem 6: $\mathbb{T_{1}} \approx \mathbb{T_{2}}$
The rings $\mathbb{T_{1}}$ and $\mathbb{T_{2}}$ are isomorphic.

**Proof:** Define mapping $\phi: \mathbb{T_{1}} \to \mathbb{T_{2}}$, $a+bi_{1}+cj_{1} \mapsto a-bi_{2}-cj_{2}$. It is trivial to see that it preserves additive structure.
$$\phi\[(a+bi_{1}+cj_{1})(d+ei_{1}+fj_{1})\] = (ad + bf + ce) - (ae + bd - cf)i_{2} - (af - be + cd)j_{2}$$
$$\begin{align}
\phi(a + bi_{1} + cj_{1})\phi(d + ei_{1} + fj_{1}) &= (a - bi_{2} - cj_{2})(d - ei_{2} - fj_{2})\\\\ &= (ad + bf + ce) - (ae + bd - cf)i_{2} - (af - be + cd)j_{2}
\end{align}$$

QED.

#### Theorem 7: $\mathbb{T_{1}} \approx \mathbb{T_{3}}$
The rings $\mathbb{T_{1}}$ and $\mathbb{T_{3}}$ are isomorphic.

**Proof:** Instead of defining the mapping and showing that there is indeed an isomorphism, for this proof I'll follow a different path and show how such mapping can be found by little trial and error. For this, first let's
look closely to the equations that define $\mathbb{T_{1}}$ and $\mathbb{T_{3}}$.
$$\begin{align}
&(1) &\hspace{0.5 cm}  &i^{3}=j^{3}=-1 \hspace{1 cm} &ij=ji=1 \hspace{1 cm} &i^{2}=-j \hspace{1 cm} &j^{2}=-i \hspace{1 cm} &\text{(Triplex numbers of the } 1^{st} \text{ kind)} \\\\
&(2) &\hspace{0.5 cm}  &i^3=ij=ji=-1   \hspace{1 cm} &j^3=1   \hspace{1 cm} &i^2=j    \hspace{1 cm} &j^2=-i   \hspace{1 cm} &\text{(Triplex numbers of the } 3^{\text{rd}} \text{ kind)} \\\\
\end{align}$$

Notice that replacing $j$ with $-j$ on $(1)$ gives us the equatons on $(2)$. Hence the mapping $a+bi_{1}+cj_{1} \mapsto a+bi_{3}-cj_{3}$ is an isomorphism.

Finally, notice that, since composition of two isomorphisms is itself an isomorphism, with this theorem, we prove that all four kinds of triplex numbers we have talked about in this blogpost are isomorphic to one another. 


## Conclusion
In this blogpost, we defined and investigated a 3D number system. We found some interesting properties and tried to understand the underlying algebraic sturcture. I think this is a good place to end this post. Thanks for reading.
