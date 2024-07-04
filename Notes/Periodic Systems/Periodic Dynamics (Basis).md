---
aliases: []
---
## Start Date: 2023-03-06

> Category: Note

Tags:
#Periodic 

Links:
[[@(hand1998)_Analytical mechanics]]


>[! Summary]
>

---
An autonomus ODE is defined as:
$$\dot x=f(x)$$
# Linearization Along a Reference Trajectory
$$x(t)=\bar{x}(t)+y(t)$$
![[Pasted image 20230307180425.png]]
where $\bar x(t)$ is the reference solution and $y(t)$ is the displacement from reference to real solution. With this the original ODE becomes:
$$\dot{x}=f(\bar{x}+y)$$
With a [[Taylor Series Expansion]]:
$$\dot{\bar{x}}+\dot{y}=f(\bar{x})+Df(\bar{x}(t))y+\mathcal{O}(|y|^2)$$
where $Df(\bar{x}(t))$ is the Jacobian of $f$ evaluated at the reference trajectory and $\mathcal{O}(|y|^{2})$ are the higher order derivatives.

The higher order derivatives can be neglected and as $\dot{x}=f(x)$ one can assume that $\dot{\bar{x}}=f(\bar{x})$ and thus:
$$\dot{y}=Df(\bar{x}(t))y$$
Define $A(t)=Df(\bar{x}(t))$ as a $n \times n$ time dependent matrix. And
$$\dot{y}=A(t)y$$
is a LTV-System.

Now the solution can be written from an initial time $t=0$ to a later time $t>0$ as:
$$y(t)=\Phi(t)y(0)$$
where $\Phi(t)$ is the state transition matrix. It is an $n \times n$ matrix obtained by solving $n^2$ ODEs written in matrix form as:
$$\dot{\Phi}=A(t)\Phi$$
with the initial condition $\Phi=I_{n\times n}$ (the idendity matrix)

# Reference Trajectory $\bar{x}(t)$ as Periodic Orbit
There is a initial displacement $y(0)$ away from the periodic orbit on a pointcare section that is transverse to $\bar{x}(t)$. 
![[FloquetDark.png]]
$$\bar{x}(t)=\bar{x}(t+T)$$
The dynamics are now linearized along the periodic orbit:
$$Df(\bar{x}(t))=Df(\bar{x}(t+T))$$
where $Df(\bar{x}(t))=A(t)=A(t+T)$

This can be solved for $\Phi(t)$ or rather in perticular for $\Phi(T)$. This is the transition matrix over one period and it is called Monodromy Matrix $M$.
$$y(T)=My(0)$$
This is a linear approximation to the pointcare map $P:\Sigma \rightarrow \Sigma$ transversal to the periodic reference orbit $\bar{x}$.

# Stability of Periodic Systems

The eigenvectors and eigenvalues of M reveal the stbility of the periodic orbit $\bar{x}$. (They reveal the phase space near the p.o.).

The eigenvalues of M ($\lambda_{1},...,\lambda_{n}$) are called the Floquet multipliers (or characteristic multipliers).

$\lambda_{i}=e^{\sigma_{i}T}$ defines a number $\sigma_i$ called Floquet exponent or characteristic exponent. $\sigma_i$ is also called a Lyaponov exponent.

As we are looking at a discrete System, the unit circle in the complex plane is the criterrion that divides stable and unstable behaviour.
![[Pasted image 20230307183611.png]]
M has $n$ eigenvalues ($\lambda_{1},...,\lambda_{n}$). $+1$ is always an eigenvector with the eigenvector pointing along the periodic orbit (evaluated at $f(\bar{x}_{0})$). Because if there is a pertubation along the periodic orbit it will produce another point that is exactly on the periodic orbit again.

Stability is determined by the remaining n-1 eigenvalues.
![[Pasted image 20230307184404.png]]
Eigenvalues with $|\lambda_i|<1$ are inside the unit circle and that coincides with stability (asymptotically stable).
$|\lambda_{i}|=1$ is on the unit circle and correspont to neutrally stable.
$|\lambda_{i}|>0$ is outside and unstable.

