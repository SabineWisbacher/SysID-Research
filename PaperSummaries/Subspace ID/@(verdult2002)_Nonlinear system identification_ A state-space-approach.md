---
aliases:
  - verdult2002
---

### Vincent Verdult(2002)

>Category: PhD
>[PDF](verdult2002.pdf)
>[Zotero-Link](zotero://select/items/@verdult2002)

>[!ABSTRACT]-
>

>[!Info]- Quotes
>S.103  SPDF-S.169
"The input signal for both data sets equals a unit-variance, zero-mean Gaussian white noise."

---
### Tags:
#example
#SubspaceIdentification 

---
### Refrences:

[[@(chen2001)_A New Subspace Identiﬁcation Method for Bilinear Systems]] [[chen2001.pdf]]

---
# Introduction

Three different state-space model structures are discussed:
	1:==linear parameter-varying system==
		Only LPV Systems in which the system matrices are an affine function of the time-varying parameter vector are considered
	2: ==bilinear system==
		This is a special case of the LPV System where the time-varying parameter equals the input signal
	3: ==weighted combination of local linear state-space models==
		Such a system can be used to approximate a very large class of nonlinear systems. If the weights are viewed as time-varying parameters, a linear parameter-varying system is obtained.

Two different types of identification methods are discussed: nonlinear optimization-based methods and subspace methods.

Subspace methods are only discussed for the linear parameter-varying
system and the bilinear system.

## LPV Systems
$$\begin{align}
x_{k+1}&=\mathcal{A}(p_{k})x_{k}+\mathcal{B}(p_k)u_{k} \ \\
y_k&=\mathcal{C}\ (p_{k})x_{k}+\mathcal{D}(p_{k})u_k
\end{align}$$
A LPV system can be viewed as a nonlinear system that is linearized along a time-varying trajectory determined by the time-varying parameter vector $p_{k}$.

### LPV Systems with affine parameter dependence
>This corresponds to polytope models? Meaning that all possible variations of the system are part of a convex mass? So if it is stable for all edge points, it remains stable for all solutions?

$$\mathcal{A}(p_{k})=A_{o}+\sum\limits_{i=1}^{s}[p_{k}]_{i}A_{i}$$
so $s$ is the number of time-varying parameter vectors and each time dependent parameter adds a part to the sum that makes up the linear differential equation.

The system then can be written like this:
$$\begin{align}
x_{k+1}&=A\left[\begin{array}{c}
x_k\\p_{k}\otimes x_k
\end{array}\right]+
B\left[\begin{array}{c}
u_k\\p_{k}\otimes u_k
\end{array}\right]
\ \\
y_{k}&=
C\left[\begin{array}{c}
x_k\\p_{k}\otimes x_k
\end{array}\right]+
D\left[\begin{array}{c}
u_k\\p_{k}\otimes u_k
\end{array}\right]
\end{align}$$
with:
$$A \coloneqq \left[\begin{array}{c}
A_{0}&A_{1}&A_{2}&\dots A_{s}
\end{array}\right]$$
$$B \coloneqq \left[\begin{array}{c}
B_{0}&B_{1}&B_{2}&\dots B_{s}
\end{array}\right]$$
$$C \coloneqq \left[\begin{array}{c}
C_{0}&C_{1}&C_{2}&\dots C_{s}
\end{array}\right]$$
$$D \coloneqq \left[\begin{array}{c}
D_{0}&D_{1}&D_{2}&\dots D_{s}
\end{array}\right]$$
>[!Note]-
>$$\mathcal{A}(p_k)=\left[\begin{array}{c}
\frac{Z_{\alpha}}{v_{trim}}v_{LPV}&Z_{q}+1 &0\\ \frac{M_{\alpha}}{v_{trim}^{2}}v_{LPV}^{2}& \frac{M_{q}}{v_{trim}}v_{LPV}&0\\0&1&0
\end{array}\right] \rightarrow
\left[\begin{array}{c}
\left[\begin{array}{c} 0&Z_{q}+1\\ 0&0\end{array}\right]
\left[\begin{array}{c} \frac{Z_q}{v_{trim}}&0\\0& \frac{M_{q}}{v_{trim}}\end{array}\right]
\left[\begin{array}{c} 0&0\\ \frac{M_{\alpha}}{v_{trim}^{2}}&0\end{array}\right]
\end{array}\right]
$$
### Linear Fractional Transformation Description

>[!Definition]+ Definition lower LFT
> Let the matrix $M \in \mathbb{R}^{(p_{1}+p_{2})\times(q_{1}+q_{2})}$ be partitioned as
> $$M = \left[\begin{array}{c|c} 
> M_{11} & M_{12}\\ \hline
> M_{21} & M_{22}
> \end{array}\right]$$
> 
> The lower LFT of $M$ with respect to the matrix $\Delta \in \mathbb{R}^{q_{2}\times p_{2}}$ is given by
> $$\mathcal{F}(M,\Delta) \coloneqq M_{11}+M_{12}\Delta(I_{p2}-M_{22}\Delta)^{-1}M_{21}$$
> 
> provided that the inverse of $(I_{p2}-M_{22}\Delta)$ exists.

A LPV system with fractional parameter dependence can be represented by the lower LFT
$$\mathcal{F}\left(\left[\begin{array}{c c|c}
A_{0}&B_{0}&B_{f}\\
C_{0}&D_{0}&D_{f}\\ \hline
C_{z}&D_{z}&D_{zf}
\end{array}\right],\Delta(p_{k})\right)$$
the time varying block being
$$\Delta(p_{k})\coloneqq \left[\begin{array}{c}
[p_{k}]_{1}I_{r1}&&&0\\
&[p_{k}]_{2}I_{r2}&&\\
&&\ddots&\\
0&&&[p_{k}]_{s}I_{rs}
\end{array}\right]$$
and the time-invariant system:
$$\begin{align}
x_{k+1}&= A_{0}x_{k}+B_{0}u_{k}+B_{f}f_{k},\\
y_{k}&=C_{0}x_{k}+D_{0}u_{k}+D_{f}f_{k},\\
z_{k}&=C_{z}x_{k}+D_{z}u_{k}+D_{zf}f_k
\end{align}$$
$$f_{k}=\Delta(p_{k})z_{k}$$
LFTs can be described as a linear time-invariant (LTI) dynamic system that has a partial feedback connection with a time-varying static block $(\Delta(p_{k}))$ 

![[Pasted image 20231211160112.png]]
![[Pasted image 20231211161847.png]]


### Relationship Between LFT and Affine Parameter Dependence

The $D_zf$ Matrix contains the coefficients that define the fractional parameter dependence if they are zero, the parameter dependence becomes affine.

In LFT form the state space equations are
$$\left[\begin{array}{c}
x_{k+1}\\y_{k}
\end{array}\right]=\mathcal{F}(M,\Delta(p_{k}))
\left[\begin{array}{c}
x_k\\y_k
\end{array}\right]$$
With
$$\mathcal{F}(M,\Delta(p_{k}))=
\left[\begin{array}{c}
A_{0}&B_{0}\\C_{0}&D_{0}
\end{array}\right]+
\left[\begin{array}{c}
B_{f}\\D_{f}
\end{array}\right]
\Delta(p_k)(I-D_{zf}\Delta(p_{k}))^{-1}
\left[\begin{array}{c}
C_{z}&D_{z}
\end{array}\right]$$

so with $D_{zf}=0$ the Equations reorder to:
$$\left[\begin{array}{c}
x_{k+1}\\y_{k}
\end{array}\right]=
\left(
\left[\begin{array}{c}
A_{0}&B_{0}\\C_{0}&D_{0}
\end{array}\right]+
\left[\begin{array}{c}
B_{f}\\D_{f}
\end{array}\right]
\Delta(p_{k})
\left[\begin{array}{c}
C_{z}&D_{z}
\end{array}\right]
\right)
\left[\begin{array}{c}
x_{k}\\u_{k}
\end{array}\right]$$
which can be rearranged to
$$\begin{align}
x_{k+1}&=
\left[\begin{array}{c}
A_{0}+B_{f}\Delta(p_{k})C_{z}
\end{array}\right]\ x_{k}+
\left[\begin{array}{c}
B_{0}+B_{f}\Delta(p_{k})D_{z}
\end{array}\right]\ u_{k}
\\
y_{k}&=
\left[\begin{array}{c}
C_{0}+D_{f}\Delta(p_{k})C_{z}
\end{array}\right]\ x_{k}+
\left[\begin{array}{c}
D_{0}+D_{f}\Delta(p_{k})D_{z}
\end{array}\right]\ u_{k}
\end{align}$$
or:
$$\begin{align}
x_{k+1}&=
\left[\begin{array}{c}
A_{0}&[B_{f,1}C_{z,1}&\dots&B_{f,s}C_{z,s}]
\end{array}\right]
\left[\begin{array}{c}
x_{k}\\p_{k}\otimes x_{k}
\end{array}\right]+
\left[\begin{array}{c}
B_{0}&[B_{f,1}D_{z,1}&\dots&B_{f,s}D_{z,s}]
\end{array}\right]
\left[\begin{array}{c}
u_{k}\\p_{k}\otimes u_{k}
\end{array}\right]
\\
y_{k}&=
\left[\begin{array}{c}
C_{0}&[D_{f,1}C_{z,1}&\dots&D_{f,s}C_{z,s}]
\end{array}\right]
\left[\begin{array}{c}
x_{k}\\p_{k}\otimes x_{k}
\end{array}\right]+
\left[\begin{array}{c}
D_{0}&[D_{f,1}D_{z,1}&\dots&D_{f,s}D_{z,s}]
\end{array}\right]
\left[\begin{array}{c}
u_{k}\\p_{k}\otimes u_{k}
\end{array}\right]
\end{align}$$

and this corresponds to the affine parameter description.

### From LFT to Affine Parameter Dependence

> I do not really understand this:

The LFT description contains the $D_{zf}$ Matrix, which displays the fractional parameter dependence.
The LPV system (with affine parameter dependence) doesn't display that dependence.

But there is a way to get an LFT description with $D_{zf}\neq 0$ out of an LTV system by redefining and adding parameters to the vector $p_{k}$.

In the LFT description, the effect of the time varying parameters is influenced in $D_{zf}$ as
$$\Delta(p_{k})(I_{r}-D_{zf}\Delta(p_{k}))^{-1}$$
whereas in the LTV description this simply reduces to:
$$\Delta(p_{k})$$
Now this can be expanded so that there is a matrix that depends linearly on the time varying parameter used in the LPV system $p_{k}$.


## Identification Methods

The LPV identification is written down for the LPV notation with (affine) parameter notation
>[!Bsp - short period of LT40]-
>$$\left[\begin{array}{c}
\dot{\alpha}\\\dot{q}
\end{array}\right]= 
\left[\begin{array}{c}
\left[\begin{array}{c} 0&Z_{q}+1\\ 0&0\end{array}\right]
\left[\begin{array}{c} \frac{Z_q}{v_{trim}}&0\\0& \frac{M_{q}}{v_{trim}}\end{array}\right]
\left[\begin{array}{c} 0&0\\ \frac{M_{\alpha}}{v_{trim}^{2}}&0\end{array}\right]
\end{array}\right]
\left[\begin{array}{l}
\left[\begin{array}{c} \alpha\\q \end{array}\right]\\
\left[\begin{array}{c} \alpha\\q \end{array}\right]v_{LPV}\\
\left[\begin{array}{c}\alpha\\q \end{array}\right]v_{LPV}^{2}
\end{array}\right]+
\left[\begin{array}{c}
\frac{Z_{dE}}{v_{trim}}\\ \frac{M_{dE}}{v_{trim}}\\0
\end{array}\right] [dE]v_{LPV}$$

### Data Equation
$$x_{k+1}=A\left[\begin{array}{c}
x_k\\p_{k}\otimes x_{k}\
\end{array}\right]+B\left[\begin{array}{c}
u_{k}\\p_{k}\otimes u_{k}
\end{array}\right]+w_{k}$$
$$y_{k}=Cx_{k}+Du_{k}+v_{k}$$
>[!Bsp: One Parameter, no noise]+
>
>$$y_{k+1}=CA_{0}x_{k}+CA_1p_{k}x_{k}+CB_{0}u_{k}+CB_{1}p_{k}u_{k}+Du_{k+1}$$
>$$\left[\begin{array}{c}
 y_{k+1}\\y_{k}
 \end{array}\right]=\left[\begin{array}{c}
 CA_{0}&CA_{1}\\C&0
 \end{array}\right]\left[\begin{array}{c}
 x_{k}\\p_{k}x_{k}
 \end{array}\right]+\left[\begin{array}{c}
 CB_{0}&CB_{1}\\D&0
 \end{array}\right]\left[\begin{array}{c}
 u_{k}\\p_{k}u_{k}
 \end{array}\right]+\left[\begin{array}{c}
 D\\0
 \end{array}\right]u_{k+1}$$
 >
>$$\begin{align}x_{k+2}=
\left[\begin{array}{c}
A_{0}^{2}&A_{0}A_{1}&A_{1}A_{0}&A_{1}^{2}
\end{array}\right]
\left[\begin{array}{c}
x_{k}\\p_{k}x_{k}\\p_{k+1}x_{k}\\p_{k+1}p_{k}x_{k}
\end{array}\right]+
\left[\begin{array}{c}
A_{0}B_{0}&A_{0}B_{1}&A_{1}B_{0}&A_{1}B_{1}
\end{array}\right]
\left[\begin{array}{c}
u_{k}\\p_{k}u_{k}\\p_{k+1}u_{k}\\p_{k+1}p_{k}u_{k}
\end{array}\right]+
\left[\begin{array}{c}
B_{0}&B_{1}
\end{array}\right]
\left[\begin{array}{c}
u_{k+1}\\p_{k+1}u_{k+1}
\end{array}\right]\end{align}$$
>
>$$\left[\begin{array}{c}
y_{k+2}\\y_{k+1}\\y_{k}
\end{array}\right]=\left[\begin{array}{c}
CA_{0}^{2}&CA_{0}A_{1}&CA_{1}A_{0}&CA_{1}^{2}\\CA_{0}&CA_{1}&0&0\\C&0&0&0
\end{array}\right]\left[\begin{array}{c}
x_{k}\\p_{k}x_{k}\\p_{k+1}x_{k}\\p_{k+1}p_{k}x_{k}
\end{array}\right]+\left[\begin{array}{c}
CA_{0}B_{0}&CA_{0}B_{1}&CA_{1}B_{0}&CA_{1}B_{1}\\CB_{0}&CB_{1}&0&0\\D&0&0&0
\end{array}\right]\left[\begin{array}{c}
u_{k}\\p_{k}u_{k}\\p_{k+1}u_{k}\\p_{k+1}p_{k}u_{k}
\end{array}\right]+
\left[\begin{array}{c}
CB_{0}&CB_{1}\\D&0\\0&0
\end{array}\right]
\left[\begin{array}{c}
u_{k+1}\\p_{k+1}u_{k+1}
\end{array}\right]
\left[\begin{array}{c}
D\\0\\0
\end{array}\right]u_{k+2}$$
>
>$$\begin{align}
x_{k+3}=
\left[\begin{array}{c}
A_{0}^{3}&A_{0}^{2}A_{1}&A_{0}A_{1}A_{0}&A_{0}A_{1}^{2}&A_{1}A_{0}^{2}&A_{1}A_{0}A_{1}&A_{1}^{2}A_{0}&A_{1}^{3}
\end{array}\right]
\left[\begin{array}{c}
x_{k}\\p_{k}x_{k}\\p_{k+1}x_{k}\\p_{k+1}p_{k}x_{k}\\p_{k+2}x_{k}\\p_{k+2}p_{k}x_k\\p_{k+2}p_{k+1}x_{k}\\p_{k+2}p_{k+1}p_{k}x_{k}
\end{array}\right]+
\left[\begin{array}{c}
A_{0}^{2}B_{0}&A_{0}^{2}B_{1}&A_{0}A_{1}B_{0}&A_{0}A_{1}B_{1}&A_{1}A_{0}B_{0}&A_{1}A_{0}B_{1}&A_{1}^{2}B_{0}&A_{1}^{2}B_{1}
\end{array}\right]
\left[\begin{array}{c}
u_{k}\\p_{k}u_{k}\\p_{k+1}u_{k}\\p_{k+1}p_{k}u_{k}\\p_{k+2}u_{k}\\p_{k+2}p_{k}u_k\\p_{k+2}p_{k+1}u_{k}\\p_{k+2}p_{k+1}p_{k}u_{k}
\end{array}\right]+
\left[\begin{array}{c}
A_{0}B_{0}&A_{0}B_{1}&A_{1}B_{0}&A_{1}B_{1}
\end{array}\right]
\left[\begin{array}{c}
u_{k+1}\\p_{k+1}u_{k+1}\\p_{k+2}u_{k+1}\\p_{k+2}p_{k+1}u_{k+1}
\end{array}\right]+
\left[\begin{array}{c}
B_{0}&B_{1}
\end{array}\right]
\left[\begin{array}{c}
u_{k+2}\\p_{k+2}u_{k+2}
\end{array}\right]
\end{align}$$
>
>$$\left[\begin{array}{c}
y_{k+3}\\y_{k+2}\\y_{k+1}\\y_{k}
\end{array}\right]=\left[\begin{array}{c}
CA_{0}^{3}&CA_{0}^{2}A_{1}&CA_{0}A_{1}A_{0}&CA_{0}A_{1}^{2}&CA_{1}A_{0}^{2}&CA_{1}^{2}A_{0}&CA_{1}^{3}\\
CA_{0}^{2}&CA_{0}A_{1}&CA_{1}A_{0}&CA_{1}^{2}&0&0&0\\
CA_{0}&CA_{1}&0&0&0&0&0\\
C&0&0&0&0&0&0
\end{array}\right]\left[\begin{array}{c}
x_{k}\\p_{k}x_{k}\\p_{k+1}x_{k}\\p_{k+1}p_{k}x_{k}\\p_{k+2}x_{k}\\p_{k+2}p_{k}x_{k}\\p_{k+2}p_{k+1}x_{k}\\p_{k+2}p_{k+1}p_{k}x_{k}
\end{array}\right]+
\left[\begin{array}{c}
CA_{0}^{2}B_{0}&CA_{0}^{2}B_{1}&CA_{0}A_{1}B_{0}&CA_{0}A_{1}B_{1}&CA_{1}A_{0}B_{0}&CA_{1}A_{0}B_{1}&CA_{1}^{2}B_{0}&CA_{1}^{2}B_{1}\\
CA_{0}B_{0}&CA_{0}B_{1}&CA_{1}B_{0}&CA_{1}B_{1}&0&0&0&0\\
CB_{0}&CB_{1}&0&0&0&0&0&0\\
D&0&0&0&0&0&0&0
\end{array}\right]
\left[\begin{array}{c}
u_{k}\\p_{k}u_{k}\\p_{k+1}u_{k}\\p_{k+1}p_{k}u_{k}\\p_{k+2}u_{k}\\p_{k+2}p_{k}u_{k}\\p_{k+2}p_{k+1}u_{k}\\p_{k+2}p_{k+1}p_{k}u_{k}
\end{array}\right]+
\left[\begin{array}{c}
CA_{0}B_{0}&CA_{0}B_{1}&CA_{1}B_{0}&CA_{1}B_{1}\\
CB_{0}&CB_{1}&0&0\\
D&0&0&0\\
0&0&0&0
\end{array}\right]
\left[\begin{array}{c}
u_{k+1}\\p_{k+1}u_{k+1}\\p_{k+2}u_{k+1}\\p_{k+2}p_{k+1}u_{k+1}
\end{array}\right]+
\left[\begin{array}{c}
CB_{0}&CB_{1}\\D&0\\0&0\\0&0
\end{array}\right]
\left[\begin{array}{c}
u_{k+2}\\p_{k+2}u_{k+2}
\end{array}\right]
\left[\begin{array}{c}
D\\0\\0\\0
\end{array}\right]u_{k+3}$$
$$\left[\begin{array}{c}
y_{k+3}\\y_{k+2}\\y_{k+1}\\y_k
\end{array}\right]=
H_{k}^{x}
\left[\begin{array}{r}
\left[\begin{array}{c}
x_{k}\\p_{k}x_{k}
\end{array}\right]
\\
p_{k+1}
\left[\begin{array}{c}
x_{k}\\p_{k}x_{k}
\end{array}\right]
\\
p_{k+2}
\left[\begin{array}{r}
\left[\begin{array}{c}
x_{k}\\p_{k}x_{k}
\end{array}\right]
\\
p_{k+1}
\left[\begin{array}{c}
x_{k}\\p_{k}x_{k}
\end{array}\right]
\end{array}\right]
\end{array}\right]+
% Building of the Input-Data-Matrix (This is the relevant part for defining the Nullspace later on)
\left[\begin{array}{c}
\left[\begin{array}{c}
CB_{0}&CB_{1}\\D&0\\0&0\\0&0
\end{array}\right]
\left[\begin{array}{c}
CA_{0}B_{0}&CA_{0}B_{1}&CA_{1}B_{0}&CA_{1}B_{1}\\
CB_{0}&CB_{1}&0&0\\
D&0&0&0\\
0&0&0&0
\end{array}\right]
\left[\begin{array}{c}
CA_{0}^{2}B_{0}&CA_{0}^{2}B_{1}&CA_{0}A_{1}B_{0}&CA_{0}A_{1}B_{1}&CA_{1}A_{0}B_{0}&CA_{1}A_{0}B_{1}&CA_{1}^{2}B_{0}&CA_{1}^{2}B_{1}\\
CA_{0}B_{0}&CA_{0}B_{1}&CA_{1}B_{0}&CA_{1}B_{1}&0&0&0&0\\
CB_{0}&CB_{1}&0&0&0&0&0&0\\
D&0&0&0&0&0&0&0
\end{array}\right]
\end{array}\right]
%--------------------------------------------------------------------------------------------------
\left[\begin{array}{r}
%Since first
\left[\begin{array}{c}
u_{k+2}\\p_{k+2}u_{k+2}
\end{array}\right]\\
%Since second
\left[\begin{array}{r}
\left[\begin{array}{c}
u_{k+1}\\p_{k+1}u_{k+1}
\end{array}\right]
\\
p_{k+2}
\left[\begin{array}{c}
u_{k+1}\\p_{k+1}u_{k+1}
\end{array}\right]
\end{array}\right]\\
%Since first timestep
\left[\begin{array}{r}
\left[\begin{array}{r}
\left[\begin{array}{c}
u_{k}\\p_{k}u_{k}
\end{array}\right]
\\
p_{k+1}
\left[\begin{array}{c}
u_{k}\\p_{k}u_{k}
\end{array}\right]
\end{array}\right]
\\
p_{k+2}
\left[\begin{array}{r}
\left[\begin{array}{c}
u_{k}\\p_{k}u_{k}
\end{array}\right]\\
p_{k+1}
\left[\begin{array}{c}
u_{k}\\p_{k}u_{k}
\end{array}\right]
\end{array}\right]
\end{array}\right]
\end{array}\right]
+
\left[\begin{array}{c}
D\\0\\0\\0
\end{array}\right] u_{k+3}$$


By separating the parameter dependent part from the LTI part the equation can be written as:
$$\mathcal{Y}_{k+j|j}=\Gamma_{k}X_{j}+\tilde{H}_{k}^{x}(P_{k+j-1|j} \odot X_{j})+H^{u}_{k}U_{k+1|j}+G_{k}^{u}U_{k+j}+H_{k}^{w}W_{k+j-1|j}+\mathcal{V}_{k+j|j}$$


