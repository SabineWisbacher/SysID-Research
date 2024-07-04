---
aliases: [SysID Toolbox]
---
## Start Date: 2023-01-20

> Category: Note

Tags:
#SubspaceIdentification 

Links:
[[@(ljung1999)_System identification_ Theory for the user]] ([[ljung1999.pdf]])

>[! Summary]
>

---
# The Subspace Algorithm in the Toolbox

The whole Idea is based on linear least square methods. The state space representation can be written as:
$$x(t+1)=Ax(t)+Bu(t)$$
$$y(t)=Cx(t)+Du(t)+v(t)$$
Given:
$Y(t)=\left[\begin{array}{c}x(t+1)\\y(t)\end{array}\right]$
$\Theta=\left[\begin{array}{c}A&B\\C&D\end{array}\right]$
$\Phi(t)=\left[\begin{array}{c}x(t)\\u(t)\end{array}\right]$
$E(t)=\left[\begin{array}{c}w(t)\\v(t)\end{array}\right]$

The representation can be written as:
$$Y(t)=\Theta\Phi(t)+E(t)$$
and thus be solved as a simple least square method.
Prior to this however, the state vector sequence $x(t)$ has to be known. 
For this some seps need to be taken:
## Step 1: Choose $s_1$, $s_{2}$, $r$ and $l$  and form $\hat{Y}_{r}(t)$ and $Y$
$$\hat{Y}_{r}(t)=\Theta_{N}\phi_{s}(t)$$
$$\hat{Y}_{r}(t)=\left[\begin{array}{c}
\hat{y}(t|t-1)\\
\vdots\\
\hat{y}(t+r-1|t-1)
\end{array}\right]$$
$$Y=\left[\begin{array}{c}
\hat{Y}_{r}(t)&\dots &\hat{Y}_{r}(N)
\end{array}\right]$$
$$\phi_{s}(t)=\left[\begin{array}{c}
y(t-1)\\
\vdots\\
y(t-s_{1})\\
u(t-1)\\
\vdots\\
u(t-s_{2})
\end{array}\right]$$

(related to the discrete linear differential equation?)
$$y(t+k-1|t-1)=\alpha_{1}y(t-1)+\dots+\alpha_{s1}y(t-s_{1})+ \beta_1u(t-1)+\dots+\beta_{s2}u(t-s_{2})$$

Solving the least squares method would thus result into the estimate of $\Theta_N$ which would contain the $\alpha$ and $\beta$ values. 

# Subspace Identificarion Functions
- ==**era**==
  Estimate state-space model from impulse response data using Eigensystem Realization Algorithm (ERA)
- ==**idss**==
  Use idss to create a continuous-time or discrete-time state-space model with identifiable (estimable) coefficients, or to convert Dynamic System Models to state-space form.
- ==**n4sid**==
  sys = n4sid(tt,nx) estimates a discrete-time state-space model sys of order nx using all the input and output signals in the timetable tt.
- ==**ssest**==
  sys = ssest(tt,nx) estimates the continuous-time state-space model sys of order nx, using all the input and output signals in the timetable tt. You can use this syntax for SISO and MISO systems. The function assumes that the last variable in the timetable is the single output signal.
- ==**ssregest**==
  sys = ssregest(tt,nx) estimates a discrete-time state-space model by reduction of a regularized ARX model, using the all the input and output signals in the timetable tt. You can use this syntax for SISO and MIMO systems. The function assumes that the last variable in the timetable is the single output signal. You can also use this syntax to estimate a time-series model if tt contains a single variable that represents the sole output. 
  For MIMO systems and for timetables that contain more variables than you plan to use for estimation, you must also use name-value arguments to specify the names of the input and output channels you want. For more information, see tt.
  To estimate a continuous-time model, set 'Ts' to 0 using name-value syntax.

## era

## idss
This function doesn't create the state space model itself, it needs n4sid or ssest to create a state space model from input output data