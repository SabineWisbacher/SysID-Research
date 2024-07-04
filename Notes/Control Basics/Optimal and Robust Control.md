---
aliases:
---
## Start Date: 2023-11-14

> Category: Note

Tags:
#ControlBasics 

Links:
https://www.youtube.com/watch?v=z64cXTZKw4I&list=PLMLojHoA_QPmRiPotD_TnfdUkglTexuqm

>[! Summary]
>

---
# Introduction to Optimization - Analysis
The core problem is always:
$$minimize\ f(x),\ x\in \mathbb{R}^{n}$$

there can be boundary conditions, x can be a vector and of course:
$$max\ f(x)=-min(-f(x))$$
## Unconstrained optimization - scalar case

A function can have a local minimum
$$\exists\ \varepsilon > 0: f(x^{*})\leq f(x^{*}+\alpha),\ |\alpha|<\varepsilon$$
where $\varepsilon$ is the range around the local minimum for which it holds.
![[Pasted image 20231114164238.png]]

The goal however is always to find the global mimimum $x^{OPT}$
