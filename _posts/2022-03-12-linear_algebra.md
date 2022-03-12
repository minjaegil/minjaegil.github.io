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
# Math for ML - Linear Algebra
This post jots down the key points of Chapter 2 Linear Algebra from [Mathmematics for Machine Learning](https://mml-book.github.io).
# 1. Matrices
## 1.1 Matrix
#### Matrix
A real-valued ($m, n$) matrix ***A***, where $m, n \in N$, is a $m\cdot n$-tuple with $m$ rows and $n$ columns.

$$ A = \begin{bmatrix}1 & 3 & 2\\3 & 2 &1\end{bmatrix} \in R^{2\times 3} $$
  
#### Identity Matrix
In $R^{n\times n}$, identity matrix ***$I_{n}$*** is a $n \times n$-matrix containing 1 on the diagonal and 0 everywhere else.

$$I_{3} = \begin{bmatrix}1 & 0 & 0\\0 & 1 &0\\0&0&1\end{bmatrix} \in R^{3\times 3}$$
  
## 1.2 Matrix Addition and Multiplication

Matrices can only be multiplied if their *neighboring* dimensions match. \
For instance, a $n\times k$-matrix ***A*** can be multiplied with a $k\times m$-matrix ***B***, but only from the left side. Thus, $BA$ will not defined if $m\neq n$.

#### Propoerties of Matrices
Associativity:

$$\forall A \in R^{m\times n}, B \in R^{n \times p}, C \in R^{p\times q}: (AB)C=A(BC):$$

Distributivity:

$$\forall A,B \in R^{m\times n}, C,D \in R^{n\times p}: (A+B)C=AC + BC$$

Multiplication with the identity matrix:



