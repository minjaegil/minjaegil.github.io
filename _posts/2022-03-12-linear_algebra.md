---
layout: single
title: "Linear Algebra"
categories: Math
tag: [matrix, vector, ML]
toc: true
toc_sticky: true
toc_label: "Contents"
use_math: true
---
# Math for ML
This post jots down the key points of Chapter 2 Linear Algebra from [Mathmematics for Machine Learning](https://mml-book.github.io).

<br>

# 1. Matrices

## 1.1 Matrix

**Matrix** 

A real-valued ($m, n$) matrix ***A***, where $m, n \in N$, is a $m\cdot n$-tuple with $m$ rows and $n$ columns.

$$ A = \begin{bmatrix}1 & 3 & 2\\3 & 2 &1\end{bmatrix} \in R^{2\times 3}$$

**Identity Matrix**

In $R^{n\times n}$, identity matrix ***$I_{n}$*** is a $n \times n$-matrix containing 1 on the diagonal and 0 everywhere else.

$$I_{3} = \begin{bmatrix}1 & 0 & 0\\0 & 1 &0\\0&0&1\end{bmatrix} \in R^{3\times 3}$$

## 1.2 Propoerties of Matrices

Matrices can only be multiplied if their *neighboring* dimensions match. \
For instance, a $n\times k$-matrix ***A*** can be multiplied with a $k\times m$-matrix ***B***, but only from the left side. Thus, ***BA*** will not defined if $m\neq n$.

- **Associativity**: &nbsp; &nbsp; $\forall A \in R^{m\times n}, B \in R^{n \times p}, C \in R^{p\times q}: (AB)C=A(BC)$

- **Distributivity**: &nbsp; &nbsp; $\forall A,B \in R^{m\times n}, C,D \in R^{n\times p}: (A+B)C=AC + BC$

- **Multiplication with the Identity Matrix**: &nbsp; &nbsp; $\forall A \in R^{m\times n}: I_{m}A=AI_{n}=A$ &nbsp; ($I_{m}\neq I_{n}$ for $m\neq n$)

## 1.3 Inverse and Transpose

**Inverse**

If two matrices $A,B \in R^{n\times n}$ have the property $AB=I_{n}=BA$, $B$ is called the *inverse* of $A$ and denoted by $A^{-1}$.  

Note that <u>not every matrix has an inverse</u>. 

$$ (A+B)^{-1}\neq A^{-1}+B^{-1}$$

$$(AB)^{-1}=B^{-1}A^{-1}$$


**Transpose**

For $A\in R^{m\times n}$ the matrix $B\in R^{n\times m}$ with $b_{ij}=a_{ji}$ is called the *transpose* of $A$ and is written as $B=A^{\top}$.

$$ (A+B)^{\top}=A^{\top}+B^{\top}$$

$$(AB)^{\top}=B^{\top}A^{\top}$$

If $A=A^{\top}$, matrix $A$ is *symmetric*.

<br>

# 2. Solving Systems of Linear Equations

## 2.1 Approach

Converting a system of equations into the compact matrix notation $Ax=b$,

1. Find a *particular solution* to $Ax=b$. 
2. Find all solutions to $Ax=0$.
3. Combine the solutions from steps 1 and 2 to get the *general solution*.

***Explanation.*** Adding 0 to our particular solution does not change the particular solution since:

$$A(x+x^{\prime})=Ax+Ax^{\prime}$$

## 2.2 Row-Echelon Form
A matrix is row-echelon form if:
- All rows that contain only zeros are at the bottom of the matrix.
- Looking at nonzero rows only, the first nonzero number from the left (also called the *pivot* or the *leading coefficient*) is always strictly to the right of the pivot of the row above it.

Example of row-echelon form matrix:

$$\begin{bmatrix}A&|&b\end{bmatrix}=\begin{bmatrix}1 & -2& 1&-1&1&|&0\\0 & 0 &1&-1&3&|&-2 \\ 0&0&0&1&-2&|&1 \\ 0&0&0&0&0&|&0\end{bmatrix}$$

**Obtaining a Particular Solution**

The row-echelon form helps to determine a particular solution. 
1. First, express the right-hand side of the equation system using the *pivot columns*: 

$$\lambda_{1} \begin{bmatrix}1 \\0 \\ 0 \\0 \end{bmatrix} + \lambda_{2} \begin{bmatrix}1 \\1 \\ 0 \\0 \end{bmatrix} +\lambda_{3} \begin{bmatrix}-1 \\-1 \\ 1 \\0 \end{bmatrix} =\begin{bmatrix}0\\ -2 \\ 1 \\0 \end{bmatrix}$$

2. Find $\lambda_3 = 1, \lambda_2 = -1,\lambda_1 = 2$
3. Put everything together <u>including the non-pivot columns</u> for which we set the coefficients implicitly to 0.
4.  Therefore, we get the particular solution $x=[2, 0, -1, 1, 0]^{\top}$.

**Reduced Row Echelon Form**

Also called row-reduced echelon form or row canonical form,
- It is in row-echelon form
- Every pivot is 1.
- The pivot is the only nonzero entry <u>in its column</u>.

Example of reduced row-echelon form matrix:

$$A=\begin{bmatrix}1 & 3 & 0 & 0 & 3\\ 0 & 0 & 1 & 0 & 9 \\ 0 &0 & 0 & 1 & -4 \end{bmatrix}$$

**Obtaining a General Solution**

The reduced row-echelon form helps to determine a particular solution. We can use the **Minus-1 Trick**:
1. Augment matrix $A$ to a $5\times 5$ matrix by adding rows of such form at the places where the pivots on the diagonal are missing: 

$$ {\widetilde{A} =\begin{bmatrix}1 & 3 & 0 & 0 & 3\\ \color{blue}0 &\color{blue} -\color{blue}1 & \color{blue}0 & \color{blue}0 & \color{blue}0\\ 0 & 0 & 1 & 0 & 9  \\ 0 &0 & 0 & 1 & -4 \\ \color{blue}0 &\color{blue} 0 & \color{blue}0 & \color{blue}0 & \color{blue}- \color{blue}1\end{bmatrix}}$$

2. Read out solutions of $Ax=0$ by taking the columns of $\widetilde{A}$, which contain $-1$ on the diagonal:

$${x\in R^5 :x=\lambda_{1} \begin{bmatrix}3 \\-1 \\ 0 \\0 \\ 0\end{bmatrix} + \lambda_{2} \begin{bmatrix}3 \\0 \\ 9 \\-4 \\-1\end{bmatrix}}$$ 

<br>

# 3. Vector Spaces

## 3.1 Groups

Consider a set $\mathcal{G}$ and an operation $\otimes:\mathcal{G}\times\mathcal{G}\rightarrow\mathcal{G}$. Then $G=(\mathcal{G},\otimes)$ is called a *group* if:

- **Closure** of $\mathcal{G}$ under $\otimes$: &nbsp; $\forall x,y \in \mathcal{G} : x \otimes y \in \mathcal{G}$
- **Associativity**: &nbsp; $\forall x,y,z \in \mathcal{G} : (x \otimes y)\otimes z = x \otimes (y \otimes z)$
- **Neutral element**: &nbsp; $\exists e \in \mathcal{G}  ,\forall x \in \mathcal{G}: x \otimes e = x$ and $e \otimes x = x$
- **Inverse element**: $\forall x \in \mathcal{G}, \exists y \in \mathcal{G} : x\otimes y = e$ and $y \otimes x = e$ where $e$ is the neutral element.

**Abelian Group**

Group $G=(\mathcal{G},\otimes)$ is called an *Abelian group* if it additionally meets the condition that $\forall x,y \in \mathcal{G}: x \otimes y = y \otimes x$ (commutative).

- $(\mathbb{Z},+)$ is an Abelian group
- $(\mathbb{N}_0 ,+)$ is not a group: &nbsp; Although it possesses a neutral element (0), the inverse elements are missing
- $(\mathbb{Z},\cdot)$ is not a group:  &nbsp; Although it possesses a neutral element (1), the inverse elements are missing
- $(\mathbb{R}, \cdot)$ is not a group since 0 doesn't possess an inverse element
- $(\mathbb{R}$ \ {0} $,\cdot)$ is Abelian
- $(\mathbb{R}^{m\times n},+)$, set of $m\times n$-metrices is Abelian
- $(\mathbb{R}^{n\times n},\cdot)$ depends on whether it has an inverse (regular) or not:
    - Neutral element: The identity matrix $I_n$ is the neutral element
    - Inverse element: If the inverse exists, then in exactly this case is a group and is also calledd the *general linear group*
    - Since matrix multiplication is not commutative, the group is not Abelian

*$\mathbb{Z}$ : set of integers  \
*$\mathbb{N}_0$: set of natural numbers including zero  \
*$\mathbb{R}$ : set of real numbers  \
*$\mathbb{R}$ \ {0} : set of real numbers excluding zero

## 3.2 Vector Spaces

**Vector Spaces**

A real-valued *vector space* $V = (\mathcal{V},+,\cdot)$ is a set $\mathcal{V}$ with two operations:
$$+: \mathcal{V}\times \mathcal{V} \rightarrow \mathcal{V}$$ 
$$\cdot: \mathbb{R}\times \mathcal{V} \rightarrow \mathcal{V}$$
*$+:$ inner operations (vector addition)  \
*$\cdot:$ outer operation (scalars)

where

1. $(\mathcal{V},+)$ is an Abelian group
2. Distributivity:  $(\lambda + \psi)\cdot x= \lambda \cdot x +  \psi \cdot x$
3. Associativity of outer operation: $\lambda \cdot (\psi \cdot x) = (\lambda  \psi) \cdot x$
4. Neutral element with respect to the outer operation: $\forall x \in \mathcal{V}: 1 \cdot x=x$

**Vector Subspaces**

Let $V = (\mathcal{V},+,\cdot)$ be a vector space and $\mathcal{U} \subseteq \mathcal{V},  \mathcal{U} \neq \phi$. Then $U = (\mathcal{U},+,\cdot)$ is called *vector subspace* of $V$.

1. $\mathcal{U} \neq \phi$, in particular: $0 \in \mathcal{U}$
2. Closure of $U$:
    - With respect to the outer operation: $\forall \lambda \in \mathbb{R}, \forall x \in \mathcal{U}:\lambda x \in \mathcal{U}$
    - With respect to the inner operation: $\forall x, y \in \mathcal{U}: x + y \in \mathcal{U}$

<br>

# 4. Linear Independence

**Linear Dependence**

A sequence of vectors $x_1, x_2, ..., x_k$ from a vector space $V$ is said to be ***linearly dependent***  if at least one scaler is not zero such that $\lambda_1x_1+\lambda_2x_2+...+\lambda_kx_k=0$ where zero denotes a zero vector. 

In other words, a set of vectors is linearly dependent if and only if one of them a *linear combination* of the others:

$$x_1=\frac{-\lambda_2}{\lambda_1}x_2+\frac{-\lambda_3}{\lambda_1}x_3+...+\frac{-\lambda_k}{\lambda_1}x_k$$

**Evaluating Linear Independence**

If a sequence of vectors is not linearly dependent, it is linearly independent. Thus, no vector in the sequence can be represented as a linear combination of the remaining vectors in the sequence. 

Some properties of linearly independent vectors:

- $k$ vectors are linearly independent or linearly dependent. There is no third option.
- If at least one of the vectors is **0** then they are linearly dependent (because the scaler can be non-zero). The same holds if two vectors are identical.
- If one vector is a multiple of another vector, it is linearly dependent.
- Row echelon form using Gaussian elimination:
    - The pivot columns indicate the vectors, which are linearly independent of the vectors on the left.
    - The non-pivot columns can be expressed as linear combinations of the pivot columns on their left.
    - All column vectors are linearly independent if and only if all columns are pivot columns.
    - Row-echelon form matrix $A$ below is an example of linearly dependent column vectors; The second column is a non-pivot column because it is three times the first column.

    $$A=\begin{bmatrix} 1&3&0 \\ 0&0&2\end{bmatrix}$$

<br>

# 5. Basis and Rank

## 5.1 Generating Set and Basis

**Generating Set**

Consider a vector space $V = (\mathcal{V},+,\cdot)$ and set of vectors $\mathcal{A} = \{x_1, ...,x_k\} \subseteq \mathcal{V}$. If every vector $v \in \mathcal{V}$ can be expressed as a linear combination of $x_1, ...,x_k$, $\mathcal{A}$ is called a *generating set* of $V$. 

The set of all linear combinations of vectors in $\mathcal{A}$ is called the *span* of $\mathcal{A}$. If $\mathcal{A}$ spans the vector space $V$, we write $V=span[\mathcal{A}]$.

**Basis**

A generating set $\mathcal{A}$ is called *minimal* if there exists no smaller set that spans $V$. Every linearly independent generating set of $V$ is minimal and is called a *basis* of $V$.

In other words, a basis is a minimal generating set and a maximal linearly independent set of vectors; Adding any other vector to this set will make it linearly dependent. 


