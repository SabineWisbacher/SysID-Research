## Start Date: 2022-12-12

> Category: Note

Tags:
#linearization  #DCM #ControlBasics 

Links:
[[@(jonkman2005)_FAST User's Guide]]

[[@(jonkman2018)_Full-System Linearization for Floating Offshore Wind Turbines in OpenFAST_ Preprint]]

[[@(jonkman2016)_FAST modularization framework for wind turbine simulation_ Full-system linearization]]

[[@(jonkman2013)_The New Modularization Framework for the FAST Wind Turbine CAE Tool]]

[[@(sprague2015)_FAST Modular Framework for Wind Turbine Simulation_ New Algorithms and Numerical Examples]]


>[! Summary]
>

---
# State Space Linearization


$$\dot{x}=Ax+Bu$$
$$y=Cx+Du$$

Let $\Delta y$, $\Delta u$, be __deviations__ from the nominal trajectory:
$$y(t)=y_{0}(t)+\Delta y$$
$$u(t)=u_{0}(t)+\Delta u$$

Taylor Series approximation:

$$f(x,u)=f(x_0,u_{0})+\frac{\delta f(x,u)}{\delta x}|_{x_{0},u_{0}}(x-x_0)+\frac{\delta f(x,u)}{\delta u}|_{x_{0},u_{0}}(u-u_{0})+end\ here$$

the higher order terms need to be neglegted. If x is a vector $\frac{\delta f (x,u)}{\delta x}$ is a Matrix (Jacobian Matrix).



$$\dot{\vec{x}} =
\left[
\begin{array}{rcl}
\frac{\delta f_{1}} {\delta x_{1}} |_{x_0,u_0}& ... & \frac{\delta f_{1}} {\delta x_{n}} |_{x_0,u_0}\\
... & ... & ... \\
\frac{\delta f_{1}} {\delta x_{n}} |_{x_0,u_0}& ... & \frac{\delta f_{n}} {\delta x_{n}} |_{x_0,u_0}\\
\end{array}
\right]
\cdot\vec{x}+
\left[
\begin{array}{rcl}
\frac{\delta f_{1}} {\delta u_{1}} |_{x_0,u_0}& ... & \frac{\delta f_{1}} {\delta u_{p}} |_{x_0,u_0}\\
... & ... & ... \\
\frac{\delta f_{1}} {\delta u_{1}} |_{x_0,u_0}& ... & \frac{\delta f_{n}} {\delta u_{p}} |_{x_0,u_0}\\
\end{array}
\right]
\cdot \Delta \vec{u}
$$
$$\Delta \vec{y} =
\left[
\begin{array}{rcl}
\frac{\delta g_{1}} {\delta x_{1}} |_{x_0,u_0}& ... & \frac{\delta g_{1}} {\delta x_{n}} |_{x_0,u_0}\\
... & ... & ... \\
\frac{\delta g_{q}} {\delta x_{n}} |_{x_0,u_0}& ... & \frac{\delta g_{q}} {\delta x_{n}} |_{x_0,u_0}\\
\end{array}
\right]
\cdot\vec{x}+
\left[
\begin{array}{rcl}
\frac{\delta g_{1}} {\delta u_{1}} |_{x_0,u_0}& ... & \frac{\delta g_{1}} {\delta u_{p}} |_{x_0,u_0}\\
... & ... & ... \\
\frac{\delta g_{q}} {\delta u_{1}} |_{x_0,u_0}& ... & \frac{\delta g_{q}} {\delta u_{p}} |_{x_0,u_0}\\
\end{array}
\right]
\cdot \Delta \vec{u}$$

>[! Attention]+
>Does it matter whether $\Delta x$ and $\Delta \dot{x}$ are used or just $x$ and $\dot{x}$ as the equations are consistent either way?


# Linearization in FAST
[[@(jonkman2016)_FAST modularization framework for wind turbine simulation_ Full-system linearization|jonkman2016]], [[@(jonkman2018)_Full-System Linearization for Floating Offshore Wind Turbines in OpenFAST_ Preprint|jonkman2018]], [[@(jonkman2013)_The New Modularization Framework for the FAST Wind Turbine CAE Tool|jonkman2013]]

The linearization of OpenFAST involves ([[@(jonkman2016)_FAST modularization framework for wind turbine simulation_ Full-system linearization|jonkman2016]],[[@(jonkman2018)_Full-System Linearization for Floating Offshore Wind Turbines in OpenFAST_ Preprint|jonkman2018]]):
1) finding an operating point (OP)
2) linearizing the underlying nonlinear equations of each module about the OP
3) linearizing the module-to-module input-output coupling relationships in the OpenFAST glue code about the OP, and
4) combining all linearized matrices into the full-system linear state-space model and exporting those matrices and the OP to a file.

## Operating Point Determination
An operating point is a static equilibrium (const. displacement), steady-state (constant velocity), or periodic steady-state (variation in response with rotor-azimuth angle) condition ([[@(jonkman2016)_FAST modularization framework for wind turbine simulation_ Full-system linearization|jonkman2016]]). It is defined by given values for the continuous-time states $x|_{op}$ , discrete-time states $x^{d}|_{op}$, and time $t|_{op}$ , for each module.
Equations that can be used to find the OP values are referenced to [[@(jonkman2013)_The New Modularization Framework for the FAST Wind Turbine CAE Tool|jonkman2013]]:
$$\dot{x}=X(x,x^{d},z,u,t),$$$$0=Z(x,x^{d},z,u,t) \text{ with } \left| \frac{\delta Z}{\delta z} \right| \neq 0, \text{ and } y=(x,x^{d},z,u,t)$$
One challenge is dealing with rotations (orientations) in the three dimensions, whoch do not reside in a linear space ([[@(jonkman2016)_FAST modularization framework for wind turbine simulation_ Full-system linearization|jonkman2016]]). Within the FAST modular framework, orientation at a given point in space and time is stored as a direction cosine matrix (DCM) ([[@(sprague2015)_FAST Modular Framework for Wind Turbine Simulation_ New Algorithms and Numerical Examples|sprague2015]]).

### Direction Cosine Matrices (DCMs)
https://www.youtube.com/watch?v=uECetjFi9jE (FL Engineering: 4 - Direction Cosine Matrices)
https://www.youtube.com/watch?v=hiSka63UXc4 (FL Engineering: 4.1 - Direction Cosine Matrices Example #1)
https://www.youtube.com/watch?v=QNk-x2ERaK8 (The Math Sorcerer:  What are Direction Cosines and Direction Angles? Full Derivation)

Rotating around the $E_{3}$-Axis:
$$\left[\begin{array}{c}
\hat{e}_{1}\\\hat{e}_2\\\hat{e}_3
\end{array}\right]=
\left[\begin{array}{c}
\cos(\theta)&\sin(\theta)&0\\
-\sin(\theta)&\cos(\theta)&0\\
0&0&1
\end{array}\right]
\left[\begin{array}{c}
\hat{E}_1\\\hat{E}_2\\\hat{E}_{3}
\end{array}\right]$$

Rotating around the $E_{2}$-Axis:
$$\left[\begin{array}{c}
\hat{e}_{1}\\\hat{e}_2\\\hat{e}_3
\end{array}\right]=
\left[\begin{array}{c}
\cos(\theta)&0&-\sin(\theta)\\
0&1&0\\
\sin(\theta)&0&\cos(\theta)
\end{array}\right]
\left[\begin{array}{c}
\hat{E}_1\\\hat{E}_2\\\hat{E}_{3}
\end{array}\right]$$

Rotating around the $E_{1}$-Axis:
$$\left[\begin{array}{c}
\hat{e}_{1}\\\hat{e}_2\\\hat{e}_3
\end{array}\right]=
\left[\begin{array}{c}
1&0&0\\
0&\cos(\theta)&\sin(\theta)\\
0&-\sin(\theta)&\cos(\theta)
\end{array}\right]
\left[\begin{array}{c}
\hat{E}_1\\\hat{E}_2\\\hat{E}_{3}
\end{array}\right]$$
The three direction cosine matrices make up the euler angle transformation.

A pertubation in rotation at the OP is defined as:
$$\Lambda =\Lambda|_{op}\ \Delta\Lambda$$


# Linearization in ASWING
