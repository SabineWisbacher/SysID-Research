---
aliases:
---
Start Date: 2024-01-04

> Category: Note

Tags:
#FlightDynamics

Links:
Modern Flight Dynamics (Schmidt2012) 

>[! Summary]
>

---
# Coordinate Systems
![[Pasted image 20240104141315.png]]
$S$ - Inertial
$E$ - Intermediate
$V$ - Vehicle/Body fixed

$$\omega_{E,S}=-\omega_{Earth}k_s$$

Transformations from one coordinate system to another are done by Direction Cosine Matrices (DCMs).

>[!Info]+ _Euler's Theorem_:
>The orientation between any two coordinate systems, or frames, can be defined in terms of, at most, three angles. $$T_{E-V}(\Phi,\Theta,\Psi)$$ So from Earth to Vehicle is: Bank-Pitch-Heading and in the other direction it is heading-pitch-bank $$T_{V-E}=T_{E-V}^T$$
# Vector Differentiation
$$\frac{d\mathbf{x}}{dt}|_{S}=\frac{d\mathbf{x}}{dt}|_{E}+\mathbf{\omega}_{E,S}\times\mathbf{x}$$
>[!Note]-
>This only changes perspective: It doesn't metter wether I am moving through space or space is moving around me
>In case of a translational movement of the body trough space this should get even easier as only its velocity needs to be taken into account and the velocity needn't be derived from angular velocity.

# Newtons Law
Newtons second law is usually stated as:
$$F=ma$$
To use it in a vector context we need to take a closer look
## Constant Mass
Translational Form:$$F=m \frac{d}{dt}|_{I}\left( \frac{d\mathbf{x}}{dt}|_{I} \right)$$
Rotational Form:$$\mathbf{x}\times \mathbf{F}=m \frac{d}{dt}|_{I}\left( \mathbf{x} \times \frac{d\mathbf{x}}{dt}|_{I} \right)$$
# Small Perturbation Theory
1. Derive Nonlinear Equations
2. Redefine the DOFs as deviations from a reference point
3. Develop Reference and Perturbation Set of Equations
4. Choose reference condition of interest
5. Analyze the perturbation behavior close to the reference condition


