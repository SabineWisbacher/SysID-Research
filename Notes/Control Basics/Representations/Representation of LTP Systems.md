## Start Date: 2022-12-08

> Category: Note

Tags:
#linearization 
#ControlBasics 

Links:
[[@(bittanti2000)_Invariant representations of discrete-time periodic systems]]
[[@(verhaegen2007)_Filtering and System Identification_ A Least Squares Approach]]

>[! Summary]
>

---
## Time Variant Representations
There are two time domain representations: state-space or input-output
([[bittanti2000.pdf]])

### State Space
The state-space representation in descret time ($t \in \mathbb{Z}$) is:

$$x(t+1)=A(t)x(t)+B(t)u(t)$$
$$y(t)=C(t)x(t)+D(t)u(t)$$
>[!Note]- Derivation of the discrete state space representation
>
>$\dot{x}(t)=A_c(t)x(t)+B_c(t)u(t)$
>$$x_{new}=\dot{x} \cdot \Delta t+x_{old}$$
>$x(t+1) = \left(A_c(t)x(t)+B_c(t)u(t)\right) \cdot \Delta t + x(t)$
>
>$x(t+1) = A_c \cdot \Delta t \cdot x + B_c \cdot \Delta t \cdot u+ x$
>
>$x(t+1)=(A_c\cdot\Delta t+I) \cdot x +B_c\cdot\Delta t \cdot u$
>
>$A_d=(A_c\cdot\Delta t + I)$ 
>$B_d=(B_c\cdot\Delta t)$


### Input-Output

The Output $y(t)$ is written as a linear combination of past values of the input up to time $t$.
$$y(t)=\sum\limits_{j=0}^{\infty}M_j(t)u(t-j)=M_0(t)u(t)+M_1(t)u(t-1)+...$$
Where $M_j(t)$ is a Matrix consisting of periodic coefficients, known as ==*periodic Marcov coefficients*==.

The Marcov coefficients are linked to the impulsive response.

## Time Invariant Reformulations
There are three options for the reformulation of a LTV model as LTI. The most common one is the ==time lifted reformulation==.  Other methods are ==cycling== and ==frequency lifted reformulation==. The frequency domain characterization  that leads to frequency lifting relies on the EMP-Regime (Exponential Modulated Periodic).

Frequency domain subspace formulation for LTP systems has not been investigated until [[@(uyanik2019)_Frequency-Domain Subspace Identification of Linear Time-Periodic (LTP) Systems|uyanik2019]]. This was based on frequency lifting.

### Time Lifting

### Cyclic Reformulation

### Frequency Lifting
