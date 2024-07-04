---
aliases: [Transition Matrix, Floquet, Monodromy]
---
## Start Date: 2023-03-06

> Category: Note

Tags:
#Floquet #Periodic 

Links:


>[! Summary]
>

---
# The Problem Statement
$\bar{x}(t)$ is a periodic orbit with Period T


$y(t)$ is the distance to a trajectory $x(t)$ that is close to the reference trajectory $\bar{x}(t)$.

This distance can be described as follows:
$$y(t)=\Phi(t)\cdot y(0)$$
This basically represents linearizied dynamics along a periodic orbit (which is the Jacobian of that orbit).
$$D\mathcal{f}(\bar{x}(t))=A(t)=A(t+T)=D\mathcal{f}(\bar{x}(t+T))$$
