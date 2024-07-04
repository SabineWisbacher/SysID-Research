---
aliases: []
---
## Start Date: 2023-03-28

> Category: Note

Tags:
#ControlBasics 

Links:
[[Stochastics]]
https://www.kalmanfilter.net/background.html

>[! Summary]
>

---
# Estimate of a Static System
A static system doesn't change it's state over a reasonable period of time.

Estimate the weight of a gold bar with unbiased scales (no systematic error, but measurement noise)

The gold bar is the System and its weight is the state. The dynamic model of that system is a constant since we assume that the weight doesn't change.

$$\hat{x}_{n,n}=\frac{1}{n}(z_{1}+z_{2}+...+z_{n-1}+z_{n})= \frac{1}{n}\sum\limits_{i=1}^{n}z_{i}$$
where $z_{n}$ is the measured value of the weight at time n.
The first index of $\hat{x}$ indicated which state is estimated and the second indicates the time at which the estimation is made.

If the weight doesn't change it can be said that:
$$\hat{x}_{n+1,n}=\hat{x}_{n,n}$$
But this is not practical for implementation as it would use a lot of CPU power (the average would need to be recalculated repeadedly)

It would be better to keep $\hat{x}_{n-1,n-1}$ and update after every single measurement.

For a static system it can be derived that:
>[!Note]- Derivation
>
>$$\hat{x}_{n,n}= \frac{1}{n}\sum\limits_{i=1}^{n}z_{i}= \frac{1}{n}\left(\sum\limits_{i=1}^{n-1}(z_{i})+z_n\right)= $$
>$$\frac{1}{n}\sum\limits_{i=1}^{n-1}(z_{i})+\frac{1}{n}z_{n}$$
>$$\frac{1}{n}\sum\limits_{i=1}^{n-1}(z_{i})= \frac{1}{n}\frac{n-1}{n-1}\sum\limits_{i=1}^{n-1}(z_{i})= \frac{n-1}{n} \frac{1}{n-1}\sum\limits_{i=1}^{n-1}(z_{i})$$
>$$\frac{1}{n-1}\sum\limits_{i=1}^{n-1}(z_{i})=\hat{x}_{n-1,n-1}$$
>$$\hat{x}_{n,n}= \frac{1}{n}z_{n}+ \frac{n-1}{n}\hat{x}_{n-1,n-1}$$
>$$\hat{x}_{n,n}=\hat{x}_{n-1,n-1}+ \frac{1}{n}(z_{n}-\hat{x}_{n-1,n-1})$$

as the system is static: $\hat{x}_{n,n-1}=\hat{x}_{n-1,n-1}$

>[!Important]+ State Update Equation:
>$$\boxed{\hat{x}_{n,n}=\hat{x}_{n,n-1}+ \frac{1}{n}(z_{n}-\hat{x}_{n,n-1})}$$
>The estimate of the current state is the predicted value of that state at the last measurement plus a factor (Kalman Gain $K_n$) the current measurement minus the predicted value of the current state.
>$$\boxed{\hat{x}_{n,n}=\hat{x}_{n,n-1}+ K_n(z_{n}-\hat{x}_{n,n-1})}$$
>$z_n-\hat{x}_{n,n-1}$ is called the "measurement residual" or =="innovation"== 
>$K_n$ denotes how much weight a new measurement has on the estimate (if $K=1/n$ the influence decreases with every new measurement and at some point it will be neglectable)

>[!Question]
>for a static system this would work however one of the measurements I use for any state?

The first estimate is a initial guess (that doesn't necessarily relay on any measurement)

# System with constant velocity
$$\dot{x}=v= \frac{dx}{dt}=const.$$

>[!Important]+ State Extrapolation Equation
>also known as **Transition Equation** or **Prediction Equation**
>$$x_{n+1}=x_{n}+\Delta t\dot{x}_{n}$$
>as velocity is constant:
>$$\dot{x}_{n+1}=\dot{x}_{n}$$

This replaces the assumtion from the static example that the next state equals the previous one.

## Modifing the State Update Equation:
1: Predict the target position at time n:
	initital range: 30 000m
	initial velocity: 40 m/s
	2: Here is how the prediction works with the State Extrapolation:
	$\hat{x}_{n,n-1}=\hat{x}_{n-1,n-1}+\Delta t\ \hat{\dot{x}}_{n-1,n-1}=30 000+5\cdot40=30200\,m$
	$\hat{\dot{x}}_{n,n-1}=\hat{\dot{x}}_{n-1,n-1}=40\,m/s$
	Now if the measured new value for the range $\hat{x}_{n,n}$ is different from the predicted value $\hat{x}_{n,n-1}$ there are two possible reasons:
	- The radar measurement is noisy
	- The aircraft velocity has changed (One can calculate how the velocity must have changed if the measurement were precice)
	
3: The State Update Equation for velocity
	$\hat{\dot{x}}_{n,n}=\hat{\dot{x}}_{n,n-1}+\beta \left(\frac{z_{n}-\hat{x}_{n,n-1}}{\Delta t} \right)$
4: The State Update Equation for position
	$\hat{x}_{n,n}=\hat{x}_{n,n-1}+ \alpha (z_{n}-\hat{x}_{n,n-1})$
	The factor $\alpha$ is constant in this case. It depends on the precition with which the position can be measured. A high alpha means that we trust the measurements of the position.