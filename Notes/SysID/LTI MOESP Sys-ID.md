---
aliases:
---
## Start Date: 2023-09-29

> Category: Note

Tags:
#SubspaceIdentification #LTI 

Links:
[[@(verhaegen2007)_Filtering and System Identification_ A Least Squares Approach]]

>[! Summary]
> MOESP - Multivariable Output-Error-State-Space


---
# Subspace Model Identification (Sec 9 S.292)
(PDF-S309)

S.293
"These Methods are based on the fact that, by storing the input and output data in structured block Hankel matrices, it is possible to retrieve certain subspaces that are related to the system matrices of the signalgenerating state-space model. "


## The Data Equation
The system is described as:
$$x(k+1)=Ax(k)+Bu(k),$$
$$y(k)=Cx(k)+Du(k)$$

The state of the system at time k is given by:
$$x(k)=A^kx(0)+\sum\limits_{i=0}^{k-1}A^{k-i-1}Bu(i)$$
>[!Note]- Derivation of $x(k)$
>
>Solution of LTI System in discrete time...


>[!Note]+
>$$y(k)=C\cdot(A^{k}x(0)+\sum_{i=0}^{k-1}A^{k-i-1}Bu(i))+Du(k)$$

with the *extended observability matrix*:
$$\mathcal{O}_{s}=CA^{k}$$

and:
$$\mathcal{T}_{s}u(k)=C\sum_{i=0}^{k-1}A^{k-i-1}Bu(i)+Du(k)$$

leading to:
$$y(k)=\mathcal{O}_sx(0)+\mathcal{T}_{s}u(k)$$

For the time-invariant system a time-shifted version of the input, state and output vectors can be related with the same matrices $\mathcal{O}_{s}$ and $\mathcal{T}_s$.
$$\begin{bmatrix}
y(k)\\y(k+1)\\...\\y(k+s-1)
\end{bmatrix}
=\mathcal{O}_{s}x(k)+\mathcal{T}_{s}
\begin{bmatrix}
u(k)\\u(k+1)\\...\\u(k+s-1)
\end{bmatrix}$$

Now we can look at this connection for different time shifts (permitted by the availability of input-output samples)
The number of samples $(N)$  must be significantly greater than the length of the signals $(s)$ wich itself has to be greater than the number of states $(n)$ 
$$\boxed{Y_{0,s,N}=\mathcal{O}_{s}X_{0,N}+\mathcal{T}_{s}U_{0,s,N}}$$



## Indentification using Impulse Input
$$u(k)=
\begin{array}
\\1, for\ k=0 \\0, for\ k>0
\end{array}$$


### Adaptation of the Data Equation

If the input signal is an impulse the data equation can be written in the form of
$$Y_{0,s,N+1}=\mathcal{O}_{s}X_{0,N+1}+\mathcal{T}_{s}
\begin{bmatrix} 1&0&\dots &0 \\ 0&0&\dots&0 \\ \vdots&\vdots&\ddots&\vdots \\ 0&0&\dots&0
\end{bmatrix}$$
Therefore:
$$Y_{1,s,N}=\mathcal{O}_{s}X_{1,N}$$


### Derivation of the System Matrices

Because $x(0)=0$, $s>n$, and $N\geq s$,the column spaces of $Y_{1,s,N}$ and $\mathcal{O}_{s}$ are  equal. ( every column of $Y_{1,s,N}$ is a linear combination of the columns of $\mathcal{O}_{s}$)
>[!Note]+
>
>$$x(k)=A^kx(0)+\sum\limits_{i=0}^{k-1}A^{k-i-1}Bu(i)$$
>z.B.
>$$x(1)=Ax(0)+\sum\limits_{i=0}^{0}A^{0-1}Bu(0)=Ax(0)+Bu(0)=Bu(0)=B$$
>$$x(2)=A^2x(0)+\sum\limits_{i=0}^{1}A^{1-0}Bu(0)+A^{1-1}Bu(1)=A^2x(0)+ABu(0)+Bu(1)=ABu(0)=AB$$
>$$X_{1,N}=[\begin{array}{lr} B &AB&A^{2}B&\dots&A^{N-1}B \end{array}]=\mathcal{C}_{N}$$

$$Y_{1,s,N}=\mathcal{O}_{s}\mathcal{C}_{N}$$

>[!Info]- Sylvester's Inequality and Equality
>
>[[Sylvester's Inequality and Equality]]
>
>If $A$ and $B$ are two matrices of the same ordern $n$, then:
>$$rank(A)+rank(B)\leq rank(AB)+n$$

$$range(Y_{1,s,N})=range(\mathcal{O}_{s})$$

![[Pasted image 20230119152312.png]]


>[!Info]- SVD
>[[Singular Value Decomposition (SVD)]]
>
>$$A=[\begin{array}{lr} 
U_{1}&U_{2}\end{array}]
\begin{bmatrix} \Sigma_1&0 \\ 0&0
\end{bmatrix}
\begin{bmatrix} V_{1}^{T} \\ V_{2}^{T}
\end{bmatrix}=U_1\Sigma_1V_{1}^{T}$$

$$Y_{1,s,N}=U_n\Sigma_nV_{n}^{T}$$
since $U_{n}$ is the column space of $Y_{1,s,N}$ 
$$U_n=\mathcal{O}_{s}T=\left[\begin{array}{cl}
C_T\\
C_TA_T\\
...\\
C_TA_T^{s-1}
\end{array}\right]$$
where T stands for the similartiy transform

>[!info]- Similarity Transform
>
>[[Similarity Transform]]
>
>Two $n\times n$ matrices $A$ and $B$ are called similar if there exists an invertible $n\times n$ matrix $P$ such that:
>$$B=P^{-1}AP$$


From the relationship between $U_n$ and $\mathcal{O}_{s}$ one can first derive the $C$-Matrix up to a similarity transform by using the first entry
$$U_n(1:l,:)=C_T$$
and in a similar fashion $A$ can be derived by comparing the entries with the corresponding next entry
$$U_n(1:(s-l)l,:)A_T=U_n(l+1:sl,:)$$
$$\left[\begin{array}{cl}
C_T\\
C_TA_T\\
...\\
C_TA_T^{s-2}
\end{array}\right]A_T=\left[\begin{array}{cl}
C_TA_T\\
C_TA_T^2\\
...\\
C_TA_T^{s-1}
\end{array}\right]$$
$$U_n(1:(s-l)l,:)^{T} \cdot U_n(1:(s-l)l,:)=A_T$$

for the $B$-Matrix $Y_{1,s,N}$ is simply replaced in the data equation by its SVD.
$$U_n\Sigma_nV_{n}^{T}=\mathcal{O}_{s}X_{1,N}=\mathcal{O}_{s}\mathcal{C}_{N}$$
as $U_n=\mathcal{O}_{s}T$ the equation simplifies to:
$$T\Sigma_nV_{n}^{T}=\mathcal{C}_{N}$$
or:
$$\Sigma_{n}V_{n}^{T}=T^{-1}\mathcal{C}_{N}=[\begin{array}{lr}B_{T}&A_TB_T&\dots&A_{T}^{N-1}B_{T}\end{array}]$$
So $B_T$ equals the first column of the matrix $\Sigma_{n}V_{n}^{T}$
$$\Sigma_{n}V_{n}^{T}(:,1)=B_T$$

The matrix $D_T$ is similar to the original system matrix and can be determined with:
$$D_T=y(0)$$

>[!Attention]+
>If there are more inputs the signal responses are only equal if the A and B Matrix were identified with that exact input signal


## Identification using general input sequences

There are still limitations on the system input...

### Adaptation of the data equation

The key is to still get rid of $\mathcal{T}_{s}U_{0,s,N}$. But since the systeme is unknown and the input is now arbitrary, an estimate for $\mathcal{T}_{s}$ is used. ([[@(viberg1995)_Subspace-based methods for the identification of linear time-invariant systems|viberg1995]])
$$\begin{array}{c}min\\\mathcal{T}_{s}\end{array}\ ||Y_{0,s,N}-\mathcal{T}_{s}U_{0,s,N}||^{2}_{F}$$
$||\cdot ||_{F}$ denotes the Frobenius Norm

>[!Question]
>Why is this a valid estimate for $\mathcal{T}_{s}$?


>[!Info]- Frobenius Norm
>
>The Frobenius norm of a matrix is the square root of the sum of squared moduli of all elements

>[!Info]- Least Square Estimation
>[[Least Square Problem]]
>

$$\hat{\mathcal{T}}_{s}=Y_{0,s,N}U^{T}_{0,s,N}(U_{0,s,N}U_{0,s,N}^{T})^{-1}$$
>[!Note]- Derivation
>$$\mathcal{T}_{s}U_{0,s,N}=Y_{0,s,N}$$
>$$\mathcal{T}_{s}U_{0,s,N}=Y_{0,s,N}^{proj,col(U_{0,s,N})}+(Y_{0,s,N}-Y_{0,s,N}^{proj,col(U_{0,s,N})})$$
>
>$$\mathcal{T}_{s}U_{0,s,N}U_{0,s,N}^{T}=Y_{0,s,N}U_{0,s,N}^T$$
>$$\mathcal{T}_{s}=Y_{0,s,N}U_{0,s,N}^{T}(U_{0,s,N}U_{0,s,N}^{T})^{-1}$$

$$Y_{0,s,N}-\hat{\mathcal{T}}_{s}U_{0,s,N}=Y_{0,s,N}(I_{N}-U_{0,s,N}^{T}(U_{0,s,N}U^{T}_{0,s,N})^{-1})U_{0,s,N}=Y_{0,s,N}\Pi^{\perp}_{U_{0,s,N}}$$

with $\Pi^{\perp}_{U_{0,s,N}}$ beeing the ==orthogonal projection onto the column space of $U_{0,s,N}$== :
$$\Pi^{\perp}_{U_{0,s,N}}=(I_{N}-U_{0,s,N}^{T}(U_{0,s,N}U^{T}_{0,s,N})^{-1})U_{0,s,N}$$

To get rid of $\mathcal{T}_{s}$ , the data equation can now be multiplied with the orthogonal projection
$$Y_{0,s,N}\Pi^{\perp}_{U_{0,s,N}}=\mathcal{O}_{s}X_{0,N}\Pi^{\perp}_{U_{0,s,N}}+\mathcal{T}_{s}U_{0,s,N}\Pi^{\perp}_{U_{0,s,N}}$$
and since $\Pi^{\perp}_{U_{0,s,N}}$ is a orthogonal projection onto $U_{0,s,N}$:
$$U_{0,s,N}\Pi^{\perp}_{0,s,N}=0$$
Thus the data equation becomes:
$$Y_{0,s,N}\Pi^{\perp}_{U_{0,s,N}}=\mathcal{O}_{s}X_{0,N}\Pi^{\perp}_{U_{0,s,N}}$$
This represents the response of the System due to the state.

>[!Attention]+
>
>The rearanged Input Matrix must be of full rank. This restricts the types of input sequences that can be used to those that provide persistant exitation

>[!Info]+ Lemma
>Given the minimal state-space system
>$$x(k+1)=Ax(k)+Bu(k)$$
>$$y(k)=Cx(k)+Du(k),$$
>if the input $u(k)$ is such that
>$$rank\left(\begin{bmatrix}X_{0,N}\\ U_{0,s,N}\end{bmatrix}\right)=n+sm$$
>then
>$$rank(Y_{0,s,N}\Pi^{\perp}_{U_{0,s,N}})=n$$
>then
>$$rank(Y_{0,s,N}\Pi^{\perp}_{U_{0,s,N}})=n$$
>and
>$$range(Y_{0,s,N}\Pi^{\perp}_{U_{0,s,N}})=range(\mathcal{O}_{s})$$

Instead of using this equation to determine the $A_T$ and $C_T$-Matrix in a similar fashion as with the impulse signal, one can use RQ factorization to make the computation a lot easier.
$$\begin{bmatrix}U_{0,s,N} \\ Y_{0,s,N} \end{bmatrix}=\begin{bmatrix}R_{11}&0&0 \\ R_{21}&R_{22}&0 \end{bmatrix}\begin{bmatrix} Q_{1} \\ Q_{2} \\ Q_{3} \end{bmatrix}$$

$R_{11}\in \mathbb{R}^{sm \times sm}$, $R_{22}\in \mathbb{R}^{sl \times sl}$
$$Y_{0,s,N}\Pi^{\perp}_{U_{0,s,N}}=R_{22}Q_2$$
$$range(R_{22})=range(\mathcal{O}_{s})$$
### Determine the System Matrices
$$R_{22}=U_{n}\Sigma_{n}V_{n}^T $$
Now $A_T$ and $C_T$ can be derived as outlined for the impulse input using the [[Singular Value Decomposition (SVD)|SVD]] of $R_{22}$.


The $B_T$ and $C_T$-Matrices can be computed together with $x_{0_{T}}$ by solving the output function of the System for a Vector representing those quantities as a [[least square problem]]:
$$y(k)=C_{T}A_{T}^{k}x_{T}(0)+\left(\sum\limits_{\tau=0}^{k-1}u(\tau)^{T} \otimes C_{T}A_{T}^{k-\tau-1} \right)vec(B_{T})+\left(u(k)^{T} \otimes I_{l} \right)vec(D_T)$$

>[!Note]- Rearrange Output Equation
>
>$$y(k)=C\cdot(A^{k}x(0)+\sum_{i=0}^{k-1}A^{k-i-1}Bu(i))+Du(k)$$
>$$y(k)=CA^{k}x(0)+C\sum\limits_{i=0}^{k-1}A^{k-i-1}Bu(i)+Du(k)$$z.B.
>$$\left[\begin{array}{lr}y_{1}(k)\\ y_2(k)\\y_3(k)\end{array}\right]=CA^{k}x(0)+C\sum\limits_{i=0}^{k-1}A^{k-i-1}B\left[\begin{array}{lr}u_{1}(i)\\ u_2(i)\end{array}\right]+D\left[\begin{array}{lr}u_{1}(k)\\ u_2(k)\end{array}\right]$$
>$$\left[\begin{array}{lr} D_{11}&D_{12}\\D_{21}&D_{22}\\D_{31}&D_{32} \end{array}\right]
 \left[\begin{array}{lr} u_1(k)\\u_2(k)\end{array}\right]=
 \left[\begin{array}{lr} D_{11}u_1(k)+D_{12}u_2(k)\\D_{21}u_1(k)+D_{22}u_2(k)\\D_{31}u_1(k)+D_{32}u_2(k) \end{array}\right]$$
>is the same as:
>$$\left(u(k)^{T}\otimes I_l\right)vec(D)=
 \left(\left[\begin{array}{lr}u_{1}(k) &u_2(k)\end{array}\right]
 \otimes
 \left[\begin{array}{lr}1&0&0\\0&1&0\\0&0&1\end{array}\right]\right)
 \left[\begin{array}{lr} D_{11}\\D_{21}\\D_{31}\\D_{12}\\D_{22}\\D_{32} \end{array}\right]=$$
 >
 >$$\left[\begin{array}{c}u_1(k)&0&0&u_2(k)&0&0\\0&u_{1}(k)&0&0&u_2(k)&0\\
 0&0&u_1(k)&0&0&u_2(k)\end{array}\right]\left[\begin{array}{lr} D_{11}\\D_{21}\\D_{31}\\D_{12}\\D_{22}\\D_{32} \end{array}\right]=$$
>
> $$\left[\begin{array}{lr} D_{11}u_1(k)+D_{12}u_2(k)\\D_{21}u_1(k)+D_{22}u_2(k)\\D_{31}u_1(k)+D_{32}u_2(k) \end{array}\right]$$

$$\phi(k)=[\begin{array}{lr}\hat{C}_{T}\hat{A_T}&\sum_{\tau=0}^{k-1}u(\tau)^{T} \otimes \hat{C}_{T}\hat{A}_{T}^{k-\tau-1}& u(k)^{T} \otimes I_{l} \end{array}]^T$$
$$\theta=\left[\begin{array}{c}x_T(0)\\vec(B_{T})\\vec(D_T)\end{array}\right]$$
$$y(k)=\phi(k)^T\theta$$
Theta can be found by solving the equation in a [[Least Square Problem|least-squares]] setting
$$\begin{array}{c}min\\\theta\end{array}\frac{1}{N}\sum\limits_{k=0}^{N-1}||y(k)-\phi(k)^T\theta||^{2}_{2}$$

For the solution of this [[least square problem]] the $\phi(k)$ and $y(k)$ data need to be reconstructed in the following form:
$$Y_N=[\begin{array}{lr}y(0)& y(1)&\dots &y(N-1)\end{array}]^{T}$$
$$\Phi_N=[\begin{array}{lr}\phi(0)& \phi(1)&\dots &\phi(N-1)\end{array}]^{T}$$
The estimate becomes (S.236/PDF-S253):
$$\hat{\theta}_{N}=\left(\frac{1}{N} \Phi^{T}\Phi_{N}\right)^{-1}\frac{1}{N}\Phi_{N}^{T}Y_{N}$$
