---
aliases: [least-squares, least squares]
---
## Start Date: 2023-01-19

> Category: Note

Tags:
#numerik 

Links:
[Least squares approximation | Linear Algebra | Khan Academy](https://www.youtube.com/watch?v=MC7l96tW8V8)

[Least squares examples | Alternate coordinate systems (bases) | Linear Algebra | Khan Academy](https://www.youtube.com/watch?v=8mAZYv5wIcE)

>[! Summary]
>

---
The least Squares Approximation is the solution to
$$A\vec{x}=\vec{b}$$
for  $\vec{x} \in \mathbb{R}^{k}$ with  $A \in \mathbb{R}^{n \times k}$ and $\vec{b} \in \mathbb{R}^{n}$ if there is no definit solution. This means that there is no  $\vec{x}$ that represents a linear combination of all entries in $A$ that reaches $\vec{b}$, in other words, $\vec{b}$ is ==not== in the column space of $A$.
$$\left[\begin{array}{c}
\vdots&\vdots&&\vdots\\
\vec{a}_{1}&\vec{a}_{2}&\dots&\vec{a}_{k}\\
\vdots&\vdots&&\vdots
\end{array}\right]\left[\begin{array}{c}
x_{1} \\ \vdots \\ x_{k}
\end{array}\right]=\vec{b}
$$
$$\vec{a}_{1}x_{1}+...+\vec{a}_{k}x_{k}=\vec{b}$$
![[leastSquare.png]]

To get as close as possible to the vector $\vec{b}$ a vector $\vec{v}$ has to be found, that is within the column space of $A$ and minimizes the following criterion:
$$min||\vec{b}-A\vec{x}^{*}||^2$$
wich is the square of the length of the distance of each element of the reachable vector $\vec{v}$ and the not reachable solution $\vec{b}$ .

The closest vector to $\vec{b}$ within the subspace of $A$ is the orthogonal projection of $\vec{b}$ onto the column space of $A$.
$$A\vec{x}^{*}=proj_{C(A)}\vec{b}$$

With 
$$A\vec{x}^{*}-\vec{b}(=proj_{C(A)}\vec{b}-\vec{b})$$
the orthogonal vector to $A$ that connects the soultion with its approximation can be found. Per definition this vector is an element of the orthogonal complement of $A$.
>[!Info]+
>The orthogonal complement is the set of everything that is orthogonal to the regarded subspace
>$$C(A)^{\perp}$$

$$A\vec{x}^{*}-\vec{b} \in C(A)^{\perp}$$

>[!Info]+
>The ortogonal complement is equal to the Nullspace of $A^T$ (or the left Nullspace of $A$)
>meaning the nullspace of the columnspace of $A$
>$$C(A)^{\perp}=N(A^T)$$

$$A\vec{x}^{*}-\vec{b}\in N(A^T)$$
>[!Info]+
>If you multiply a matrix with its orthogonal complement, you'll end up with a matrix that is either the identity matrix or a zero matrix.
>
>The orthogonal complement of a matrix is a subspace of the vector space that is orthogonal (perpendicular) to the original matrix. When you multiply a matrix with its orthogonal complement, you're projecting the matrix onto this subspace, which means that all the information that is orthogonal to the subspace is lost. If the subspace is of the same dimension as the original matrix, then the result will be an identity matrix. If the subspace is of lower dimension, then the result will be a zero matrix, indicating that all the information in the original matrix has been lost.

$$A^T(A\vec{x}^*-\vec{b})=0$$
Rearranged this gives
$$A^{T}A\vec{x}^*-A^{T}\vec{b}=0$$
$$A^{T}A\vec{x}^{*}=A^{T}\vec{b}$$
so
$$\vec{x}^{*}=(A^{T}A)^{-1}A^{T}\cdot \vec{b}$$
