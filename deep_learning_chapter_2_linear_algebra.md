
# Chapter 2 Linear Algebra, Deep Learning

## 2.1 Scalars, vectors, matrices, and tensors

* Scalar:
    * They are written in italic.
    * They have lowercase variable names.
    * When introduced you specify what they are.
$$x$$
* Vectors:
    * An array of numbers.
    * They are written in lowercase and in bold.
    * When identifying an element in a vector the vector is written in italic with a subscript identifying the particular element.
    * You also need to say what kind of numbers are in the vector.
    * If you want to retrieve all elements except a certain element(s), you can use the subscript operator, with a `-` in front of it.
$$ x = \begin{bmatrix} a\\b\\c\\d \end{bmatrix} $$
* Matrices:
    * Each element is identified with two indices instead of one.
    * Matrices have uppercase variable names and are in bold.
    * All numbers in a row or column can be identified with a `:`.
$$ 
x = \begin{bmatrix} a & b\\c & d \end{bmatrix} 
$$
* Tensors:
    * A tensor is any array that has more then two axes.
$$ 
x = 
\begin{bmatrix}
\begin{bmatrix} a & b\\c & d \end{bmatrix} 
\begin{bmatrix} a & b\\c & d \end{bmatrix} \\
\begin{bmatrix} a & b\\c & d \end{bmatrix} 
\begin{bmatrix} a & b\\c & d \end{bmatrix} 
\end{bmatrix}
$$

### Transpose
The transpose of a matrix is the mirror image of a matrix across a diagonal line, called the main line. It runs down from the top left to the bottom right.
Denoted as: $x^\top$

Vectors can be thought of as matrices with one column. The *transpose* of a vector is a matrix with only one row.

Matrices can be added together as long as they have the same shape.

You can add a scalar to a matrix or multiply it by a matrix, using element wise operations.

You can add a vector to a matrix. A vector can be multiplied or add to a matrix, either column wise or row wise.

## 2.2 Multiplying matrices and vectors
A matrix product of matrices $A$ and $B$ is a third matrix $C$, where $A$ must have the same number of columns as $B$ has rows. Example: $A = m * n$, $B = n * p$, $C = m * p$; $C = AB$.
The product operation is defined as:
$$ 
C_{i,j} = \sum_k A_{i,k} B_{k,j}
$$

When conducting element-wise multiplication with two matrices, this is known as the **Hadamard product**, and is denoted as: $A \odot B$. 

The dot product of two vectors of the same dimensions is the matrix product of $x^\top y$.

The following are valid matrix operations:
Matrix multiplication is distributive.
$$ A(B+C) = AB + AC $$
...and associative.
$$ A(BC) = (AB)C $$
It is not communtative, $BA = AB$ does not always hold, however the dot product between two vectors is.
$$ x^\top y = y^\top x $$

The transpose of a matrix product has a simple form.
$$ (AB)^\top = B^\top A^\top $$

## 2.3 Identity and inverse matrices
An identity matrix is a matrix that does not change any vector when we multiply that vector by that matrix, denoted as $I_n$.

An identity matrix is simple: all the entries along the main diagonal are 1 and all other entries are 0. 
$$
\begin{bmatrix} 1&0&0\\0&1&0\\0&0&1 \end{bmatrix}
$$

## 2.4 Linear dependence and span (Don't currently fully understand this chapter, so I just copied it, for the most part)
For $A^{-1}$ to exist, the following equation must have exactly one solution for every value of $b$: $Ax = b$. It is also possible for the system of equations to have no solutions or infinitely many solutions for some values of $b$. It is not possible, however, to have more than one  but less than infinitely many solutions for a particular $b$; if both $x$ and $y$ are solutions then: $z = \alpha x + (1-\alpha)y$, is also a solution for any real $\alpha$.

To analyze how many solutions the equation has, think of the columns of $A$ as specifying different directions we can travel in from the origin, then determine how many ways there are of reaching $b$. In this view, each element of $x$ specifies how far we should travel in each of these directions, with $x_i$ specifying how far to move in the direction of column i:
$$ 
Ax = \sum_i x_i A_{:,i} 
$$

In general this kind of operation is called a linear combination. Formally, a linear combination of some set of vectors ${v^{(1)},...,v^{(n)}}$ is given by multiplying each vector $v^{(i)}$ by a corresponding scalar coefficient and adding the results: 
$$
\sum_ic_iv^{(i)}
$$
The span of a set of vectors is the set of all points obtainable by linear combination of the original vectors.

Determining whether $Ax=b$ has a solution thus amounts to testing whether $b$ is in the span of the columns of $A$.This particular span is known as the column space, or the range, of $A$.

In order for the system $Ax=b$ to have a solution for all values of $b\in \mathbb{R}^m$, we therefore require that the column space of $A$ be all of $\mathbb{R}^m$. If any point in $\mathbb{R}^m$ is excluded from the column space, that point is a potential value of $b$ that has no solution. The requirement that the column space of $A$ be all of $\mathbb{R}^m$ implies immediately that $A$ must have at least $m$ columns, that is, $n\ge m$. Otherwise, the dimensionality of the column space would be less than $m$. For example, consider a $3\times2$ matrix. The target $b$ is 3-D, but $x$ is only 2-D, so modifying the value of $x$ at best enables us to trace out a 2-D plane within $\mathbb{R}^3$. The equation has a solution if and only if b lies on that plane.

Having $n\le m$ is only a necessary condition for every point to have a solution. It is not a sufficient condition, because it is possible for some of the columns to be redundant. Consider a $2\times2$ matrix where both of the columns are identical. This has the same column space as a $2\times1$ matrix containing only one copy of the replicated column. In other words, the column space is still just a line and fails to encompass all of $\mathbb{R}^2$, even though there are two columns.

Formally, this kind of redundancy is known as linear dependence. A set of vectors is linearly independent *if no vector in the set is a linear combination of the other vectors*. If we add a vector to a set that is a linear combination of the other vectors in the set, the new vector does not add any points to the set's span. This means that for the column space of the matrix to encompass all of $\mathbb{R}^m$, the matrix must contain at least one set of $m$ linearly independent columns. This condition is both necessary and sufficient for equation 2.11 to have a solution for every value of $b$. Note that the requirement is for a set to have exactly $m$ linearly independent columns, not at least $m$. No set of $m$-dimensional vectors can have more than $m$ mutually linearly independent columns, but a matrix with more than $m$ columns may have more than one such set.

For the matrix to have an inverse, we additionally need to ensure that equation 2.11 has at most one solution for each value of $b$. To do so, we need to make certain that the matrix has at most $m$ columns. Otherwise there is more than one way of parameterizing each solution.

Together, this means that the matrix must be square, that is, we require that $m=n$ and that all the columns be linearly independent. A square matrix with linearly dependent columns is known as a singular.

If $A$ is not square or is square but singular, solving the equation is still possible, but we cannot use the method of matrix inversion to find a solution.

So far we have discussed matrix inverses as being multiplied on the left. It is also possible to define as inverse that is multiplied on the right:
$$ AA^{-1}=I$$
For square matrices, the left inverse and right inverse are equal.

## 2.5 Norms
Sometimes we need to measure the size of a vector. In machine learning, we usually measure the size of vectors using a function call a **norm**. Formally, the $L^p$ norm is given by:
$$
\Vert x\Vert_p=(\sum_i|x_i|^p)^{\frac{1}{p}}
$$

for $p \in\mathbb{R}, p \ge1$.

This is the equation for the $L^2$ norm, which is so common that is is often denoted as just $\Vert x\Vert$, omitting the $2$. Above just replace the $p$ with $2$ and it becomes as such.

It is also known as the **Euclidean norm**, which is simply the Euclidean distance from the origin to the point identified by $x$.

Norms including the $L^p$ norm, are functions mapping vectors to non-negative values. On an intuitive level, the norm of a vector $x$ measures the distance from the origin to the point $x$. More rigorously, a norm is *any function $f$ that satisfies the following properties:*
* $f(x)=0\Rightarrow x = 0$
* $f(x+y)\le f(x)+f(y)$ The triangle inequality
* $\forall\alpha\in\mathbb{R},f(\alpha x)=|\alpha|f(x)$

The squared $L^2$ norm is more convenient to work with mathematically and computationally than the $L^2$ norm itself. For example each derivative of the squared $L^2$ norm with respect to each element of $x$ depends only on the corresponding element of $x$, while all the derivatives fo the $L^2$ norm may be undesirable because it increases very slowly near the origin. In several machine learning applications, it is important to discriminate between elements that are exactly zero and elements that are small but nonzero. In these cases, we turn to a function that grows at the same rate in all locations, but that retains mathematical simplicity: the $L^1$ norm. The $L^1$ norm may be simplified to:
$$
||x||_1=\sum_i|x_i|
$$
The $L^1$ norm is commonly used when the difference between zeros and nonzeros is very important. every time an element of $x$ moves away from 0 by $\epsilon$, the $L^1$ norm increases by $\epsilon$.

We sometimes measure the size of the vector by counting its number of nonzero elements. Some authors refer to this function as the "$L^0$ norm," but this is incorrect terminology. The number of nonzero entries in a vector is not a norm, because scaling the vector by $\alpha$ does not change the number of nonzero entries. The $L^1$ norm is often used as a substitute for the number of nonzero entries.

One other norm that commonly arises in machine learning is the $L^\infty$ norm, also known as the max norm. This norm simplifies to the absolute value of the element with the largest magnitude in the vector,
$$
||x||_\infty= \begin{matrix}max\\i\end{matrix}|x_i|
$$

Sometimes we may also wish to measure the size of a matrix. In the context of deep learning, the most common way to do this is with the otherwise obscure **Frobenius norm**:
$$
||A||_F=\sqrt{\sum_{i,j}A^2_{i,j}}
$$
which is analogous to the $L^2$ norm of a vector.

The dot product of two vectors can be rewritten in term of norms. Specifically,
$$
x^\top y=||x||_2||y||_2\cos\theta
$$
...where $\theta$ is the angle between $x$ and $y$.

## 2.6 Special kinds of matrices and vectors
Diagonal matrices consist mostly of zeros and have nonzero entries only along the main diagonal. Formally, a matrix $D$ is diagonal if and only if $D_{i,j}=0$ for all $i\neq j$. We write $diag(v)$ to denote a square diagonal matrix whose diagonal entries are given by the entries of the vector $v$. Multiplying diagonal matrices is computationally efficient. To compute $diag(v)x=v\odot x$. Inverting a square diagonal matrix is also efficient. The inverse exists only if every diagonal entry is nonzero. You can obtain a less expensive (and less descriptive) machine learning algorithm by restricting some matrices to be diagonal.

It is possible to construct non-square diagonal matrices, although they do not have an inverse. 

A symmetric matrix is any matrix equal to its own transpose: $A=A^\top$.

Symmetric matrices often arise when the entries are generated by some function of two arguments that does not depend on the order of the arguments. For example, if $A$ is a matrix of distance measurements, with $A_{i,j}$ giving the distance from point $i$ to point $j$, then $A_{i,j}=A_{j,i}$ because distance functions are symmetric.

A unit vector is a vector with unit norm: $||x||_2=1$.

A vector $x$ and a vector $y$ are orthogonal if, $x^\top y=0$. If both vectors have a nonzero norm, this means that they are at a 90 degree angle to each other. In $\mathbb{R}^n$, at most $n$ vectors may be mutually orthogonal with nonzero norms. If the vectors not only are orthogonal but also have unit norm, we call them orthonormal.

An orthogonal matrix is a square matrix whose rows are mutually orthonormal and whose columns are mutually orthonormal:
$$
A^\top A=AA^\top=I
$$
This implies that
$$
A^{-1}=A^\top
$$
so orthogonal matrices are of interest because their inverse is very cheap to compute. 

## 2.7 Eigendecomposition
One of the most widely used kinds of matrix decomposition is called eigen-decomposition, in which we decompose a matrix into a set of eigenvectors and eigenvalues.

An eigenvector of a square matrix $A$ is a nonzero vector $v$ such that  multiplication by $A$ alters only the scale of $v$: $Av=\lambda v$.

The scalar $\lambda$ is known as the eigenvalue corresponding to this eigenvector. One can also find a left eigenvector such that a left eigenvector such that $v^\top A=\lambda v^\top$, but we are usually concerned with right eigenvectors.

If $v$ is an eigenvector of $A$, then so is any rescaled vector $sv$ for $s\in\mathbb{R},s\ueq0$. Moreover, $sv$ still has the same eigenvalue. For this reason, we usually look ony for unit eigenvectors.

Suppose that a matrix $A$ has $n$ linearly independent eigenvectors ${v^{(1)},...,v^{(n)}}$ with corresponding eigenvalues {\lambda_1,...,\lambda_n}. We may concatenate all the eigenvectors to form a matrix $V$ with one eigenvector per column: $V=[v^{(1)},...,v^{(n)}]$. Likewise, we can concatenate the eigenvalues to form a vector $\mathbf{\lambda}=[\lambda_1,...,\lambda_b]^\top$. The eigendecomposition of $A$ is then given by: $A=Vdiag(\mathbf{\lambda})V^{-1}$.

We have seen that constructing matrices with specific eigenvalues and eigenvectors enables ust to stretch space in desired directions. Yet we often want to decompose matrices into their eigenvalues and eigenvectors. Doing so can help us analyze certain properties of the matrix, much as decomposing an integer into its prime factors can help us understand the behavior of that integer.

Not every matrix can be decomposed into eigenvalues and eigenvectors. In some cases, the decomposition exists but involves complex rather than real numbers. Fortunately, in this book, we usually need to decompose only a specific class of matrices that have a simple decomposition. Specifically, every real symmetric matrix can be decomposed into an expression using only real-valued eigenvectors and eigenvalues: $A=Q\Lambda Q^\top$, where $Q$ is an orthogonal matrix composed of eigenvectors of $A$, and $\Lambda$ is a diagonal matrix. The eigenvalue $\Lambda_{i,i}$ is associated with the eigenvector in column $i$ of $Q$, denoted as $Q_{:,i}$. Because $Q$ is an orthogonal matrix, we can think of $A$ as scaling space by $\lambda_i$ in direction $v^{(i)}$.

While any real symmetric matrix $A$ is guaranteed to have an eigendecomposition, the eigendecomposition may not be unique. If any two or more eigenvectors share the same eigenvalue, then any set of orthogonal vectors lying in their span are also eigenvectors with that eigenvalue, and we could equivalently choose a $Q$ using those eigenvectors instead. By convention, we usually sort the entries of $\Lambda$ in descending order. Under this convention, the eigendecomposition is unique only if all the eigenvalues are unique.

The eigendecomposition of a matrix tells us many useful facts about the matrix. The matrix is singular if and only if any of the eigenvalues are zero. Teh eigendecomposition of a real symmetric matrix can also be used to optimize quadratic expressions of the form $f(x)=x^\top Ax$ subject to $||x||_2=1$. Whenever $x$ is equal to an eigenvector of $A$, $f$ takes on the value of the corresponding eigenvalue. The maximum value of $f$ within the constraint region is the maximum eigenvalue and its maximum value within the constraint region is the minimum eigenvalue.

A matrix whose eigenvalues are all positive is called positive definite. A matrix whose eigenvalues are all positive or zero valued is called positive semi-definite. Likewise, if all eigenvalues are negative, the matrix is negative definite, and if all eigenvalues are negative or zero valued, it is negative semi-definite. Positive semi-definite matrices are interesting because they guarantee that $\forall x, x^\top Ax\ge0$. Positive definite matrices additionally guarantee that $x\top Ax=0\Rightarrow x=0$.

## 2.8 Singular value decomposition
The singular value decomposition provides another way to factorize a matrix, into singular vectors and singular values. The SVD enables us to discover some of the same kind of information as the eigendecomposition reveals; however, the SVD is more generally applicable. Every real matrix has a singular value decomposition, but the same is not true for of the eigenvalue decomposition. For example, if a matrix is not square, the eigendecomposition is not defined, and we must use a singular value decomposition instead.

Recall that the eigendecomposition involves analyzing a matrix $A$ to discover a matrix $V$ of eigenvectors and a vector of eigenvalues $\mathbf{\lambda}$ such that we can rewrite $A$ as: $A=V diag(\mathbf{\lambda})V^{-1}$.

The singular value decomposition is similar, except this time we will write $A$ as a product of three matrices: $A=UDV^\top$.

Suppose that $A$ is an $m\times n$ matrix. Then $U$ is defined to be an $m\times m$ matrix, D to be an $m\times n$ matrix, and $V$ to be an $n\times n$ matrix.

Each of these matrices is defined to have a special structure. The matrices $U$ and $V$ are both defined to be orthogonal matrices. The matrix $D$ is defined to be a diagonal matrix. Note that $D$ is not necessarily square.

The elements along the diagonal of $D$ are known as the singular values of the matrix $A$. The columns of $U$ are known as the left-singular vectors. The columns of $V$ are known as the right-singular vectors.

We can actually interpret the singular value decomposition of $A$ in terms of the eigendecomposition of functions of $A$. The left-singular vectors of $A$ are the eigenvectors of $AA^\top$. The right singular vectors of $A$ are the eigenvectors of $A^\top A$. The nonzero singular values of $A$ are the square roots of the eigenvalues of $A^\top A$. The same is true for $AA^\top$.

Perhaps the most useful feature of the SVD is that we can use it to partially generalize matrix inversion to non-square matrices, as we will see in the next section.

## 2.9 The moore-penrose pseudoinverse
Matrix inversion is not defined for matrices that are not square. Suppose we want to make a left-inverse $B$ of a matrix $A$ so that we can solve a linear equation: $Ax=y$, by left-multiplying each side to obtain: $x=By$.

Depending on the structure of the problem, it may not be possible to design a unique mapping from $A$ to $B$.

If $A$ is taller than it is wide, then it is possible for this equation to have no solution. If $A$ is wider than it is tall, then there could be multiple possible solutions.

The Moore-Penrose pseudoinverse enables us to make some headway in these cases. The pseudoinverse of $A$ is defined as a matrix: 
$$
A^+= _{\alpha\searrow 0}^{\lim} (A^\top A+\alpha I)^{-1}A^\top
$$.
Practical algorithms for computing the pseudoinverse are based not on this definition, but rather the formula: $A^+=VD^+U^\top$, where $U$, $D$, and $V$ are the singular value decomposition of $A$, and the pseudoinverse $D^+$ of a diagonal matrix $D$ is obtained by taking the reciprocal of its nonzero elements then taking the transpose of the resulting matrix.

When $A$ has more columns than rows, then solving a linear equation using the psuedoinverse provides one of the many possible solutions. Specifically, it provides the solution $x=A^+y$ with minimal Euclidean norm $||x||_2$ among all possible solutions.

When $A$ has more rows than columns, it is possible for there to be no solution. In this case, using the pseudoinverse gives us the $x$ for which $Ax$ is as close as possible to $y$ in terms of Euclidean norm $||Ax-y||_2$.

## 2.10 The trace operator
The trace operator gives the sum of all the diagonal entries of a matrix: 
$$
Tr(A)=\sum_i A_{i,i}
$$.

Writing an expression in terms of the trace operator opens up opportunities to manipulate the expression using many useful identities. For example, the trace operator is invariant to the transpose operator: $Tr(A)=Tr(A^\top)$

The trace of a square matrix composed of many factors is also in variant to moving the last factor into the first position, if the shapes of the corresponding matrices allow the resulting product to be defined: $Tr(ABC)=Tr(CAB)=Tr(BCA)$, or more generally,
$$
Tr(\prod_{i=1}^nF^{(i)})=Tr(F^{(n)}\prod_{i=1}^{n-1}F^{(i)})
$$.

This invariance to cyclic permutation holds even if the resulting product has a different shape. For example, for $A\in\mathbb{R}^{m\times n}$ and $B\in\mathbb{R}^{n\times m}$, we have: $Tr(AB)=Tr(BA)$, even though $AB\in\mathbb{R}^{m\times m}$ and $B A \in \mathbb{R}^{n\times n}$. Another useful fact to keep in mind is that a scalar is its own trace: $a=Tr(a)$.

## 2.11 The determinant
The determinant of a square matrix, denoted $det(A)$, is a function that maps matrices to real scalars. The determinant is equal to the product of all the eigenvalues of the matrix. The absolute value of the determinant can be thought of as a measure of how much multiplication by the matrix expands or contracts space. If the determinant is 0, then space is contracted completely along at least one dimension, causing it to lose all its volume. If the determinant is 1, then the transformation preserves volume.

## 2.12 Example: Principal component analysis