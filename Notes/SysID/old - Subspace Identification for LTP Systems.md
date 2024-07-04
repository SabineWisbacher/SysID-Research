## Start Date: 2023-01-19

> Category: Note

Tags: 

Links:

[[@(bittanti2009a)_Periodic Systems]] - [[bittanti2009a.pdf]]

[[@(verhaegen1995)_A class of subspace model identification algorithms to identify periodically and arbitrarily time-varying systems]] - [[verhaegen1995.pdf]]


>[! Summary]
>

>[!Question]+ Open Questions
> - [ ]  The Criterion of constant exitation? (How does it effect the number of models)
> - [ ]  How do I work with different timesteps?
> - [ ]  Is the rearrangement of data correct (does it satisfy the Gradient condition?)

---
# Subspace Identification in General
Subspace Identification Techniques (not only for LTI Systems) are largly based on the derivation of the data equation form of the output formula and the elimination of the input influence on that equation([[@(verhaegen2007)_Filtering and System Identification_ A Least Squares Approach|verhaegen2007]]).

[[@(verhaegen2007)_Filtering and System Identification_ A Least Squares Approach]]

# The Periodic Identification Problem in Time Domain
The periodic system in discrete state space representation takes the form of
$$x(t+1)=A(t)x(t)+B(t)u(t)$$
$$y(t)=C(t)x(t)+D(t)u(t)$$
The solution of the state equation is given by ([[@(bittanti2009a)_Periodic Systems|bittanti2009a]])
$$x(t)=\Phi_A(t,\tau)x(\tau)+\sum\limits_{j=\tau}^{t-1}\Phi_A(t,j+1)B(j)u(j)$$
The state tansition matrix is thereby structured as follows:
$$\Phi_A(t,\tau)=\{\begin{array}{cr}
A(t-1)A(t-2)\dots A(\tau)&,\ t>\tau
\\I&,\ t=\tau
\end{array}$$
the state transition matrix and monodromy matrix come from the Floquet Theory that deals with a free-input periodic system


For this system a similarity transform can be formulated such that ([[@(verhaegen1995)_A class of subspace model identification algorithms to identify periodically and arbitrarily time-varying systems|verhaegen1995]]):
$$\left[\begin{array}{lr}
\alpha_{t}&\gamma_{t}\\\beta_{t}&\delta_{t}
\end{array} \right]=
\left[\begin{array}{lr}
T^{-1}_{t}&0\\0&I_{m}
\end{array} \right]
\left[\begin{array}{lr}
A_{t}&C_{t}\\B_{t}&D_{t}
\end{array} \right]
\left[\begin{array}{lr}
T_{t+1}&0\\0&I_t
\end{array} \right]$$
>[!Note]-
>
>|              |       |     |                   |                   |     |                          |                   |
| ------------ | ----- | --- | ----------------- | ----------------- | --- | ------------------------ | ----------------- |
|              |       |     | $A_t$             | $C_t$             |     | $T_{t+1}$                | $0$               |
|              |       |     | $B_t$             | $D_t$             |     | $0$                      | $I_t$             |
|              |       |     |                   |                   |     |                          |                   |
| $T_{t}^{-1}$ | $0$   |     | $T^{-1}_{t}A_{t}$ | $T_{t}^{-1}C_{t}$ |     | $T_{t}^{-1}A_{t}T_{t+1}$ | $T_{t}^{-1}C_{t}$ |
| $0$          | $I_m$ |     | $B_t$             | $D_{t}$           |     | $B_{t}T_{t+1}$           | $D_{t}$           |

This similarity transform preserves the boundedness and stability od the system.

So the deterministix state space identification problem becomes:
$$\xi_{j,t+1}=\xi_{j,t}\alpha_t+u_{j,t}\beta_t$$
$$y_{j,t}=\xi_{j,t}\gamma_t+u_{j,t}\delta_t$$
>[!Attention]-
>
>
>State, input and output Vectors are row vectors in this case, an alternative would be to say:
>$$\xi_{j,t+1}=\alpha_{t}^{T}\xi_{j,t}+\beta_{t}^{T}u_{j,t}$$
>$$y_{j,t}=\gamma_{t}^{T}\xi_{j,t}+\delta_{t}^{T}u_{j,t}$$
>where the state, input and output vectors would be column vectors
>![[subspace structure.png]]
>
>in this case the state space representation in Data Equation form has the following realationship:
>
>$$\left[\begin{array}{c}
y_{j_{0},t}&y_{j_{0}+1,t}&\dots&y_{j_{0}+n-1,t} \\
y_{j_{0},t+1}&\dots&\dots&y_{j_{0}+n-1,t+1} \\
\vdots&\vdots&\dots&\vdots\\
y_{j_{0},t+T-1}&y_{j_{0}+1,t+T-1}&\dots&y_{j_{0}+n-1,t+T-1}
\end{array}\right]=$$
>$$\left[\begin{array}{c}
C_t\\C_{t+1}A_{t}\\\vdots\\C_{t+T-1}\prod_{i=t}^{t+T-2}A_{i}
\end{array}\right]
\left[\begin{array}{c}
x_{j_{0},t}&x_{j_{0}+1,t}&\dots &x_{j_{0}+n-1,t}
\end{array}\right]+$$
>$$\left[\begin{array}{c}
D_t&0&0&\dots&0\\
C_{t+1}B_{t}&D_{t+1}&0&\ddots&0\\
C_{t+2}A_{t+1}B_t&C_{t+2}B_{t+1}&D_{t+2}&\ddots&0\\
\vdots&\ddots&\ddots&\ddots&\vdots\\
C_{t+T-1}\left(\prod_{i=t+1}^{t+T-2}A_{i}\right)B_t&\dots&\dots&\dots&D_{t+T-1}
\end{array}\right]
\left[\begin{array}{c}
u_{j_{0},t}&u_{j_{0}+1,t}&\dots&u_{j_{0}+n-1,t} \\
u_{j_{0},t+1}&\dots&\dots&u_{j_{0}+n-1,t+1} \\
\vdots&\vdots&\dots&\vdots\\
u_{j_{0},t+T-1}&u_{j_{0}+1,t+T-1}&\dots&u_{j_{0}+n-1,t+T-1}
\end{array}\right]$$
>
>or more compactly as:
>$$Y_{t,T}=\Theta_{t,T}X_{t}+\Delta_{t,T}U_{t,T}$$
>
>$T$ in this case denotes the number of samples during one period (how many matrices per period)
>$j$ is the idicater that shows the how maniest period is looked at ($j_0$ is the first period)

## Determination of the row space of $\Theta_{t,s}$
### First the RQ factorization of the combined rearranged data matrices is determined
$$\left[\begin{array}{Cc}
U_{t,s} \\Y_{t,s}
\end{array}\right]=
\left[\begin{array}{c}
R_{11,t}&0\\R_{21,t}&R_{22,t}
\end{array}\right]
\left[\begin{array}{c}
Q_{1,t}\\Q_{2,t}
\end{array}\right]$$
$$U_{t,s}=R_{11,t}Q_{1,t}$$
$$Y_{t,s}=R_{21,t}Q_{1,t}+R_{22,t}Q_{2,t}$$


$$\left[\begin{array}{Cc}
U_{t,s} \\X_{t,s}
\end{array}\right]=
\left[\begin{array}{c}
R_{11,t}&0\\R_{x21,t}&R_{x22,t}
\end{array}\right]
\left[\begin{array}{c}
Q_{1,t}\\Q_{x2,t}
\end{array}\right]$$
$$X_{t,s}=R_{x21,t}Q_{1,t}+R_{x22,t}Q_{x2,t}$$


### Then the resulting equations are used to simplify the data equation
$$Y_{t,s}=\Theta_{t,s}X_{t}+\Delta_{t,s}U_{t,s}$$
$$R_{21,t}Q_{1,t}+R_{21,t}Q_{2,t}=\Theta_{t,s}R_{x21,t}Q_{1,t}+\Theta_{t,s} R_{x22,t}Q_{x2,t}+\Delta_{t,s}R_{11,t}Q_{1,t}=$$
$$\left(\Theta_{t,s}R_{x21,t}+\Delta_{t,s}R_{11,t}\right)Q_{1,t}+\Theta_{t,s}R_{x22,t}Q_{x2,t}$$
under the condition that:
$$Q_{1,t}Q_{1,t}^T=I$$
$$Q_{2,t}Q_{1,t}^{T}=0$$
$$Q_{x2}Q_{1,t}^T=0$$
the equation can be multiplied with $Q_{1,t}^{T}$ and results in:
$$R_{21,t}=\Theta_{t,s}R_{x21,t}+\Delta_{t,s}R_{11,t} \tag{1}$$
which can be inserted in the left side of the RQ-data-equation
$$R_{22,t}Q_{2,t}=\Theta_{t,s}R_{x22,t}Q_{x2,t}$$
### The Resulting Row Space
$$range(R_{22,t})=range(\Theta_{t,s})$$
with
$$R_{22,t}=\left[\begin{array}{c}
U_{1,t}&U_{2,t}
\end{array}\right]
\left[\begin{array}{c}
\Sigma_t&0\\0&0
\end{array}\right]
\left[\begin{array}{c}
V_{1,t}^T\\V_{2,t}^T
\end{array}\right]$$
## Finding $\alpha_t$ and $\gamma_t$

$$\gamma_{t}=U_{1,t}(1:l,:)$$
$$\alpha_{t}\cdot U_{1,t}(l+1:end,:)=U_{1,t+1}(1:end-l,:)$$
## Finding $\beta_t$ and $\delta_t$ 
using
$$U_{2,t}^{T}\Theta_{t,s}=0\ \ assuming\ \ U_{1,t}=T^{-1}_{t}\Theta_{t,s}$$
then if eq. (1) is multiplied with $U_{2,t}^{T}$ the result is:
$$U_{2,t}^{T}R_{21,t}R_{11,t}^{-1}=U_{2,t}^{T}\Delta_{t,s}=\phi_t$$
since $\left(\left(U_{2,t}^{T}\right)^{\dagger}U_{2,t}\right)\neq 0\ or\ I$  the equation is:
$$\left(U_{2,t}^T\right)^{\dagger}U_{2,t}^{T}R_{21,t}R_{11,t}^{-1}=\left(U_{2,t}^T\right)^\dagger\phi_t=\Delta_{t,s}$$
>[!Note]- Sketch
>![[Delta-mat.png]]
>![[DeltaMat2.png]]

The most reliable entries of the reconstructed $\Delta_{t,s}$-Matrix are in the last row
>[!Question]- Why are the other entries less reliable
>(and is it still like that if $NoDTpS \neq 1$)?

>[!Note]- Sketch
>![[DeltaMatGet.png]]

>[!Attention]+ The ID doesn't work yet for $NoDTpS \neq 1$
>This means that the SysID is only valid if the number of samples per period equals the number of timesteps within that period

## Accounting for output errors
$$x_{j,t+1}=A_{t}x_{j,t}+B_{t}u_{j,t}$$
$$z_{j,t}=C_{t}x_{j,t}+D_{t}u_{j,t}+v_{j,t}$$
with $z_{j,t}$ beeing the measured output data.
With $V_{t,s}$ representing the Hankel matrix constructed from $v_{j,t}$ as seen for $u_{j,t}$ and $U_{t,s}$ before, the data equation is given by
$$Z_{t,s}=\Theta_{t,s}X_t+\Delta_{t,s}U_{t,s}+V_{t,s}$$

As $v_{j,t}$ is independent of the input and has mean zero:
$$\lim_{n\rightarrow\infty}=\frac{1}{n}U_{t2,r}V_{t1,s}^{T}=0,\ \ \  \forall t1,t2\ \ \ if\ \ \ \forall r>0\ \ \ and\ \ \  \forall s>0$$
Every input sequenz multiplied with the noise at any point over the number of experiments reaches zero if the number of experiments goes to infinity. 

![[Pasted image 20230322133016.png]]

Each entry is the sum of $n$ multiplications of the input signal at time $t_{2}+...$ in all experiments with the noise at time $t_{1}+...$ in all experiments.
(If $u$ was a constant: $u\cdot \sum\limits_{i=1}^{n} v_{i}$ and  $\frac{1}{n}\sum\limits_{i=1}^{n}v_i=mean(v)$)
With the definitions:
$$\left[\begin{array}{c}
U_{t,s}\\Z_{t,s}
\end{array}\right]=\left[\begin{array}{c}
R_{11}&0\\R_{z1,t}&R_{z2,t}
\end{array}\right]\left[\begin{array}{c}
Q_{1,t}\\Q_{z2,t}
\end{array}\right]$$
$$\left[\begin{array}{c}
U_{t,s}\\X_{t}
\end{array}\right]=\left[\begin{array}{c}
R_{11}&0\\R_{x1,t}&R_{x2,t}
\end{array}\right]\left[\begin{array}{c}
Q_{1,t}\\Q_{x2,t}
\end{array}\right]$$

this can be formulated as:
$$\frac{1}{n}U_{t,s}V_{t,s}^{T}= \frac{1}{n}R_{11}Q_{1,t}V_{t,s}^{T}=O_n(\varepsilon)$$
with $O_{n}(\varepsilon)$ beeing a matrix quantity of norm $\varepsilon$ which vanished as $n\rightarrow \infty$ 
other definitions are:
$$\lim_{n\rightarrow\infty}\frac{1}{n}V_{t,s}V_{t,s}^T=R_{v}$$
$$\lim_{n\rightarrow\infty} \frac{1}{n}X_{t}V_{t,s}^{T}=0$$
$$\lim_{n\rightarrow\infty} \frac{1}{n}R_{x2}R_{x2}^T$$

# The Periodic Identification Problem in Frequency Domain (harmonic transfer functions)

[[@(uyanik2019)_Frequency-Domain Subspace Identification of Linear Time-Periodic (LTP) Systems|uyanik2019]]
[[@(wereley1990a)_Analysis and control of linear periodically time varying systems|wereley1990a]]

