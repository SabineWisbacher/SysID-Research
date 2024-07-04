---
aliases:
---
## Start Date: 2023-09-15

> Category: Note

Tags:
#SubspaceIdentification #Periodic #LPV

Links:
[[@(verhaegen1995)_A class of subspace model identification algorithms to identify periodically and arbitrarily time-varying systems]] - [[verhaegen1995.pdf]]

[[@(bittanti2009a)_Periodic Systems]] - [[bittanti2009a.pdf]]

[[@(verdult2002)_Nonlinear system identification_ A state-space-approach]] - [[verdult2002.pdf]]

>[! Summary]
>

---
# MOESP Periodically
The concept is descriped in [[@(verhaegen1995)_A class of subspace model identification algorithms to identify periodically and arbitrarily time-varying systems|verhaegen1995]]. In the paper all equations are written with the state, input and output vector in row form. In this note however they will be written in column form.

At the core of the system is the reformulation of the periodic system in a gridded form:
>[!Note]- Reformulation of the periodic Sytem
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

This basically just sais that I can list every output over one period and write down all the equations for it in Matrix form and then do the same thing with the next period for which the equations would be the same as long as there is no shift in the starting point.

The solution in any case takes the general form of ([[@(bittanti2009a)_Periodic Systems|bittanti2009a]]):
$$y(t)=C(t)\Phi_A(t,\tau)x(\tau)+C(t)\sum\limits_{j=\tau}^{t-1}\Phi_A(t,j+1)B(j)u(j)+D(t)u(t)$$
with $t$ and $\tau$ defining the timespan between the initial value and the current value.
$$Y_{t,s}=\Theta_{t,s}X_{t}+\Delta_{t,s}U_{t,s}$$
$$\left[\begin{array}{Cc}
U_{t,s} \\Y_{t,s}
\end{array}\right]=
\left[\begin{array}{c}
R_{11,t}&0\\R_{21,t}&R_{22,t}
\end{array}\right]
\left[\begin{array}{c}
Q_{1,t}\\Q_{2,t}
\end{array}\right]$$
$$\left[\begin{array}{Cc}
U_{t,s} \\X_{t,s}
\end{array}\right]=
\left[\begin{array}{c}
R_{11,t}&0\\R_{x21,t}&R_{x22,t}
\end{array}\right]
\left[\begin{array}{c}
Q_{1,t}\\Q_{x2,t}
\end{array}\right]$$
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
$$range(R_{22,t})=range(\Theta_{t,s})$$

$$R_{22,t}=\left[\begin{array}{c}
U_{1,t}&U_{2,t}
\end{array}\right]
\left[\begin{array}{c}
\Sigma_t&0\\0&0
\end{array}\right]
\left[\begin{array}{c}
V_{1,t}^T\\V_{2,t}^T
\end{array}\right]$$
