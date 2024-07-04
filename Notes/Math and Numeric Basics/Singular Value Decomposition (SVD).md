---
aliases: [SVD]
---
## Start Date: 2023-01-16

> Category: Note

Tags: #SVD #numerik 

Links:
[[@(verhaegen2007)_Filtering and System Identification_ A Least Squares Approach|verhaegen2007]] S.26-27

>[! Summary]
>$$A=[\begin{array}{lr} 
U_{1}&U_{2}\end{array}]
\begin{bmatrix} \Sigma_1&0 \\ 0&0
\end{bmatrix}
\begin{bmatrix} V_{1}^{T} \\ V_{2}^{T}
\end{bmatrix}=U_1\Sigma_1V_{1}^{T}$$
>
>As $U$ contains the eigenvectors of $AA^{T}$, it represents the column space of the decomposed matrix


---
$$A=U\Sigma V^{T}$$
where:
- $U$ contains all the eigenvectors of $AA^T$ 
- $\Sigma \Sigma^T$ contains the eigenvalues of $AA^{T}$ ($\Sigma^{T} \Sigma$ contains the eigenvalues of $A^{T}A$) 
- $V$ contains the eigenvectors of $A^{T}A$
$$AA^{T}=U\Sigma V^{T}V\Sigma^T U^T=U\Sigma\Sigma^{T}U^{T}$$
$$A^{T} A=V\Sigma^{T}U^{T}U\Sigma V^{T}=V\Sigma^{T}\Sigma V^{T}$$

>[!Note]+
>The rank of a matrix equals the number of its linearly independent eigenvectors
>meaning:
>If $A$ has rank $r$ and thus $r$ linearly independant eigenvectors ans $r$ non-zero eigenvalues, $U$ has $r$ linearly independent columns and $r$ non-zero entries on its diagonal
>
>e.g.
>$A \in \mathbb{R}^{m\times n}$ and $rank(A)=r$ with $r<m$, $r<n$
>
>$$A=[\begin{array}{lr} 
U_{1}&U_{2}\end{array}]
\begin{bmatrix} \Sigma_1&0 \\ 0&0
\end{bmatrix}
\begin{bmatrix} V_{1}^{T} \\ V_{2}^{T}
\end{bmatrix}=U_1\Sigma_1V_{1}^{T}$$

As $U$ contains the eigenvectors of $AA^{T}$, it represents the column space of the decomposed matrix