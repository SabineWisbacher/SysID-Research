---
aliases: [Floquet, Monodromy Matrix]
---
## Start Date: 2023-01-23

> Category: Note

Tags:
#Periodic 

Links:
https://www.youtube.com/watch?v=veJJ6EiiOeo

>[! Summary]
>

---
A free-input time periodic system is considered:
$$x(t+1)=A(t)x(t)$$
$A(t)$ has constant dimension $n \times n$

The solution to this is given by:
$$x(1)=A(1)x(0)$$
$$x(2)=A(2)x(1)=A(2)A(1)x(0)$$
and so on (until one period is over and $x(0)=x(\tau)$)

Hence the solution in a more general form is:
$$x(t+1)=\Phi(t)x(t)$$
with
$$\Phi(t,\tau)=\{\begin{array}{cr}
A(t-1)A(t-2)\dots A(\tau)&,\ t>\tau
\\I&,\ t=\tau
\end{array}$$
