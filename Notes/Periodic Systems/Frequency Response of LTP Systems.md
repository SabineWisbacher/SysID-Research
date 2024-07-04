## Start Date: 2022-12-15

> Category: Note

Tags:
#Periodic 

Links:
[[@(wereley1990a)_Analysis and control of linear periodically time varying systems|wereley1990a]]

>[! Summary]
>

---
"In steady state, the repsonse of a linear time invariant (LTI) system to a ==complex exponential (sinusoidal)== input of a given frequency, is a ==complex exponential output signal== of the same frequency, but with possibly different amplitude and phase. This leads to the notion of the LTI frequency response and the LTI transfer function."

"An important characteristic of the LTI transfer function is that it is an operator for which the input and the output signal spaces are equal, that is, the space of the ==complex exponential signals==."

For LTP systems the complex exponential input signal does not lead to such a convenient frequency response notion.

>[!note]- Example for LTP Frequency Response
>consider the following LTP System:
>$$y(t)=(1-2\beta \cos(\omega_{p}t))\cdot u(t)$$
>excited with a complex exponential input signal:
>$$u(t)=e^{st}$$
>the system response is:
>$$y(t)=e^{st}-2\beta e^{st} \cos(\omega_{p}t)$$
>$$cos(\omega_{p}t)=\frac{e^{(\omega_{p}t)i}+e^{\omega_{p}t}}{2}$$
>$$y(t)=e^{st}-\beta e^{(s+\omega_{p}i)t}-\beta e^{(s-\omega_{p}i)t}$$

## Review of the LTI Frequency Response

$$\dot{x}(t)=Ax(t)+Bu(t)$$
$$y(t)=Cx(t)+Du(t)$$
The test signal for the LTI Signal is a complex exponential or the  exponentially modulated sinusoid.
$$u(t)=u_{0}e^{st},\ s\in \mathbb{C}, u_{0} \in \mathbb{C}^m$$

The total state response of a LTI System is given by the convolution form of the variation of constants formula:
$$x(t)=e^{At} \xi_{0}+\int_{0}^{t}e^{A(t-\tau)}Bu(\tau)\ d\tau$$
>[!Note]- The Cauchy Problem
>A method of solving inhomogeneous linear ordinary differential systems (or equations) resulting in the ==general solution==.
>$$\dot{x}=A(t)x+f(t),\ x(t_{0})=x_{0}$$
>where:
>
>$$A:(\alpha,\beta) \rightarrow Hom(\mathbb{R}^{n},\mathbb{R}^{n}),$$
>$$f:(\alpha, \beta) \rightarrow \mathbb{R}^{n}$$
>
>$\Phi(t)$ is the ==fundamental solution== of the homogeneous system:
>$$\dot{y}_{h}=A(t)y_{h}$$
>and
>$$y=\Phi(t)c,\ c \in \mathbb{R}^n$$
>is the ==general solution== associated with $\Phi(t)$.
>
>The method of variation of constants consists of a change of variable in the original differential equation
$$x=\Phi(t)u$$>this leads to the Cauchy formula for the solution:
>$$x=\Phi(t)\Phi^{-1}(t_{0})x_{0}+\Phi(t)\int_{t_{0}}^{t}\Phi^{-1}(\tau)f(\tau)d\tau$$



