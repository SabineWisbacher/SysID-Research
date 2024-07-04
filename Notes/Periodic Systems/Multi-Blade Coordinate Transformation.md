---
aliases: [MBC]
---
## Start Date: 2023-05-04

> Category: Note

Tags:
#Periodic 

Links:
[[@(bir2008)_Multi-Blade Coordinate Transformation and its Application to Wind Turbine Analysis]]
([[bir2008.pdf]])

[[@(padfield2018)_Helicopter flight dynamics_ Including a treatment of tiltrotor aircraft]] 
([[padfield2018.pdf]])

[[@(johnson2013)_Rotorcraft Aeromechanics]] ([[johnson2013.pdf]])


>[! Summary]
>

---
# Transformation of Coordinates

The transformation shifts the degrees of freedom from a coordinate system that rotates with the blades to a fixed non-rotating coordinate system for the whole rotor and back. It is a linear transformation.

The non-rotating degrees of freedem are introduced as:
$$x_{0}= \frac{1}{N}\sum\limits_{m=1}^{N}x^{(m)}$$
$$x_{nc}= \frac{2}{N}\sum\limits_{m=1}^{N}x^{(m)}\cos(n\psi_{m})$$
$$x_{ns}= \frac{2}{N}\sum\limits_{m=1}^{N}x^{(m)}\sin(n\psi_{m})$$
$$x_{N/2}= \frac{1}{N}\sum\limits_{m=1}^{N}x^{(m)}(-1)^{m}$$
The corresponding rotating degrees of freedom are:
$$x^{(m)}=x_{0}+\sum\limits_{n}
(x_{nc}\cos(n\psi_{m})+x_{ns}\sin(n\psi_{m})+x_{N/2} (-1)^{m})$$
The summation over the harmonic index $n$ goes from 1 to:
$$\begin{array}{l}
(N-1)/2,\ \ for\ N\ odd\\(N-2)/2,\ \ for\ N\ even\\
\end{array}$$
## Transformation in Matrix form

$$x_{rot}=\left[\begin{array}{c}
x^{(1)}&x^{(2)}& \dots&x^{(N)}
\end{array}\right]^{T}$$
$$x_{non}=\left[\begin{array}{c}
x_{0}&x_{nc}& x_{ns}&x_{N/2}
\end{array}\right]^{T}$$
$$x_{rot}=Tx_{non}$$
$$T(m,:)=\left[\begin{array}{c}
1&\cos(n\psi_{m})&\sin(n\psi_{m})&(-1)^{m}
\end{array}\right]$$
### Collective Input:
![[Pasted image 20230505152928.png]]
### Cosine Input
![[Pasted image 20230505153124.png]]

### Sinusoidal Input
![[Pasted image 20230505153732.png]]

### Second Mode of Rotor
![[Pasted image 20230505154131.png]]

### Everything Together
![[Pasted image 20230505154437.png]]

## Higher Frequency Input



## Controlls with MBC
