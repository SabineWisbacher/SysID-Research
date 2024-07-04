---
aliases: [yin2021a]
---
### Mingzhou Yin, Andrea Iannelli, Roy S. Smith(2021)

> Category: Paper
> [PDF](yin2021a.pdf)
> [Zotero-Link](zotero://select/items/@yin2021a)

>[!ABSTRACT]-
>This paper proposes a new methodology for subspace identification of linear time-periodic (LTP) systems with periodic inputs. This method overcomes the issues related to the computation of frequency response of LTP systems by utilizing the frequency response of the time-lifted system with linear time-invariant structure instead. The response is estimated with an ensemble of input-output data with periodic inputs. This allows the frequency-domain subspace identification technique to be extended to LTP systems. The time-aliased periodic impulse response can then be estimated and the order-revealing decomposition of the block-Hankel matrix is formulated. The consistency of the proposed method is proved under mild noise assumptions. Numerical simulation shows that the proposed method performs better than multiple widely-used time-domain subspace identification methods when an ensemble of periodic data is available.

---
### Tags:

#SubspaceIdentification 
#CatC 

---
### Refrences:

10 - [[@(verhaegen1995)_A class of subspace model identification algorithms to identify periodically and arbitrarily time-varying systems]]

12 - [[@(hench1995)_A technique for the identification of linear periodic state-space models]]

17 - [[@(bittanti2009a)_Periodic Systems]]


---
### Manual for Frequency-domain subspace identification of LTP systems with periodic inputs
The paper gives step by step introductions on how to identifiy the state space system from the input output data

#### 1: Lift the input-output data

The lifted output formula is given as:
$${\tilde{u}^{i}}(k)=\left[ {u^{i}}^{\top}(kP),\ {u^{i}}^{\top}(kP+1),\ ...,\  {u^{i}}^{\top} (kP+P-1)\right]^{\top}$$
$u \in \mathbb{R}^{n_{u}}$ - ($n_{u}$ is the number of input channels)
$i=1,2,...,J$ - (denodes the index of the experiments)
$NP$ is the length of the periodic inpust (simulation length) $(N \in \mathbb{N}_{+})$ 
$P$ is the period length of the System

$J \geq Pn_{u}$ - the number of experiments needs to be greater or equal to the Period length times the number of input channels

>[!Question]-
>How do the input signals for each experiment need to look like? Incresed frequency? harmonics?

>[!Note]-
>The notation and condition only make sense if: $(T=P\Delta t)$
>This leads to a structure like this:
>$$\tilde{u}(k)=
\begin{bmatrix} 
\vec u(kP)\\
\vec u(kP+\Delta t)\\
...\\
\vec u(kP+\Delta t (P-1)) \end{bmatrix}$$
>for every experiment

This results in a matrix depending on $k$ for input and output. 

>[!example]+ Example
> For three input channels ($n_u=3$) and two output channels ($n_y=2$) measured every $0.5s$ over $k$ periods of the considered system that have a period length of $2s$.
> 
> $$\tilde{u}^i(k)=
> \begin{bmatrix}
u_{1}^{i}(1.5k)& u_{2}^{i}(1.5k) & u_{3}^{i}(1.5k)\\
u_{1}^{i}(1.5k+0.5)& u_{2}^{i}(1.5k+0.5) & u_{3}^{i}(1.5k+0.5)\\
u_{1}^{i}(1.5k+1)& u_{2}^{i}(1.5k+1)& u_{3}^{i}(1.5k+1)\\
u_{1}^{i}(1.5k+1.5)& u_{2}^{i}(1.5k+1.5) &  u_{3}^{i}(1.5k+1.5)\end{bmatrix}$$
>with every ==**row**== representing one fixed operating point within the period of the system (e.g rotor position (with constant angular velosity) )
>and every ==**column**== representing one input channel.
>
>the measured output gets rearanged in a similar manner:
>$$\tilde{y}^i(k)=
 \begin{bmatrix}
y_{1}^{i}(1.5k)& y_{2}^{i}(1.5k)\\
y_{1}^{i}(1.5k+0.5)& y_{2}^{i}(1.5k+0.5)\\
y_{1}^{i}(1.5k+1)& y_{2}^{i}(1.5k+1)\\
y_{1}^{i}(1.5k+1.5)& y_{2}^{i}(1.5k+1.5)\end{bmatrix}$$
>
>with every ==**row**== representing one fixed operating point within the period of the system (e.g rotor position (with constant angular velosity) )
>and every ==**column**== representing one output channel.



#### 2: Estimate the frequency Response of the liftet system from the liftet input output data

First the Discrete Fourier Transform of the liftet input and output data on each operating point and for every input and output channel is applied (capturing the behaviour (magnitude and phase shift) of the System at each operating point over k-Periods?)
$$U_i(e^{j\omega_{k}})=\sum\limits_{n=0}^{N-1} \tilde{u}^{i}(n) e^{-\frac{2\pi nk}{N} j}$$
>[!Note]- Computation of the DFT (FFT)
>See Note on : [[FFT Computation]]

>[!example]+ Continuing the previous example
>
> The dimensions of the input and output matrices stay the same but every element now represents a fourier coefficient (complex number that captures magnitude and phase)
> $$U_{i}=
\begin{bmatrix}
U_{1,1}^{i}& U_{1,2}^{i}& U_{1,3}^{i}\\
U_{2,1}^{i}& U_{2,2}^{i}& U_{2,3}^{i}\\
U_{3,1}^{i}& U_{3,2}^{i}& U_{3,3}^{i}\\
U_{4,1}^{i}& U_{4,2}^{i}& U_{4,3}^{i}\end{bmatrix}$$
>with every row again representing one operating point and each column representing one input channel.
>
>Again similar for output:
>$$Y_i=
\begin{bmatrix}
Y_{1,1}^{i}& Y_{1,2}^{i}\\
Y_{2,1}^{i}& Y_{2,2}^{i}\\
Y_{3,1}^{i}& Y_{3,2}^{i}\\
Y_{4,1}^{i}& Y_{4,2}^{i}\end{bmatrix}$$

The data for each experiment ($i=1,2,...,J$) is now composed in the Matrices $\tilde{U}$ and $\tilde{Y}$ like this:
$$\tilde{U}=[U_{1}\ U_{2}\ ...\ U_{J}]$$
$$\tilde{Y}=[Y_{1}\ Y_{2}\ ...\ Y_{J}]$$
>[!example]+ Continuing the previous example
>
>$$\tilde{U}=\left[
\begin{bmatrix}
U_{1,1}& U_{1,2}& U_{1,3}\\
U_{2,1}& U_{2,2}& U_{2,3}\\
U_{3,1}& U_{3,2}& U_{3,3}\\
U_{4,1}& U_{4,2}& U_{4,3}\end{bmatrix}_{1}
\begin{bmatrix}
U_{1,1}& U_{1,2}& U_{1,3}\\
U_{2,1}& U_{2,2}& U_{2,3}\\
U_{3,1}& U_{3,2}& U_{3,3}\\
U_{4,1}& U_{4,2}& U_{4,3}\end{bmatrix}_{2}
...
\begin{bmatrix}
U_{1,1}& U_{1,2}& U_{1,3}\\
U_{2,1}& U_{2,2}& U_{2,3}\\
U_{3,1}& U_{3,2}& U_{3,3}\\
U_{4,1}& U_{4,2}& U_{4,3}\end{bmatrix}_{J}
\right]$$
>
>$$\tilde{Y}= \left[
\begin{bmatrix}
Y_{1,1}& Y_{1,2}\\
Y_{2,1}& Y_{2,2}\\
Y_{3,1}& Y_{3,2}\\
Y_{4,1}& Y_{4,2}\end{bmatrix}_{1}
\begin{bmatrix}
Y_{1,1}& Y_{1,2}\\
Y_{2,1}& Y_{2,2}\\
Y_{3,1}& Y_{3,2}\\
Y_{4,1}& Y_{4,2}\end{bmatrix}_{2}
...
\begin{bmatrix}
Y_{1,1}& Y_{1,2}\\
Y_{2,1}& Y_{2,2}\\
Y_{3,1}& Y_{3,2}\\
Y_{4,1}& Y_{4,2}\end{bmatrix}_{J}
\right]$$

The frequency response estimate is then given as:
$$\hat{G}(e^{j\omega_{k}})=\tilde{Y}(e^{j\omega_{k}})\tilde{U}^{\dagger} (e^{j\omega_{k}})$$
Where $\tilde{U}^{\dagger}$ is the ==right== pseudoinverse. 

>[!Note]+ Definition of the right pseudoinverse
>[Pseudo-inverse | Real Statistics Using Excel (real-statistics.com)](https://www.real-statistics.com/linear-algebra-matrix-topics/pseudo-inverse/#:~:text=Using%20the%20SVD%20method,then%20transposing%20the%20resulting%20matrix.)
>
>Considering the case where the matrix U has full rank (rank of U=min(m,n)) 
>
>If $m \leq n$, then $UU^{T}$ is invertible and $U^{\dagger}=U^{T}(UU^T)^{-1}$ 
>
>with $UU^{\dagger}=I$ 
>
>in this case $U^{\dagger}$ is the ==right== pseudoinverse

For the right pseudoinverse to have full rank: $J \geq Pn_{u}$ 

>[!Note]+ Checking dimensions
>
>$\tilde{U} \in \mathbb{C}^{P \times Jn_{u}}$ 
>$\tilde{U}^{T} \in \mathbb{C}^{Jn_{u} \times P}$ 
>$(UU^{T})^{-1} \in \mathbb{C}^{P\times P}$
>$\tilde{U}^{\dagger} \in \mathbb{C}^{Jn_{u}\times P}$
>$\tilde{Y} \in \mathbb{C}^{P \times Jn_{y}}$ 
>
>$\tilde{Y}\tilde{U}^{\dagger}$ only works if $n_{u}=n_{y}$ (output controlability?)
>then:
>$\hat{G} \in \mathbb{C}^{P\times P}$ 

