---
aliases: [becker2023]
---

### Alex Becker(2023)

>Category: Book
>[PDF](becker2023.pdf)
>[Zotero-Link](zotero://select/items/@becker2023)

>[!ABSTRACT]-
>

---

### Tags:
#CatA 
#KalmanFilter

---
### Refrences:


---

# 0 Essential Background
The theory of Kalman Filtering is based on stochastics.
## 0.1 One Dimensional Stochastics
### 0.1.1 Mean & Expected Value
The expected value (E) is the value one would expect the hidden variable to have over a long time or many trials.
The mean is only the mathematical average of a list of measurements.
$$\mu=\frac{1}{N}\sum\limits_{n=1}^{N}x_{n}$$
### 0.1.2 Variance and Standard Deviation
The variance shows the spreading of the data set from its mean.
$$\sigma^{2}=\frac{1}{N}\sum\limits_{n=1}^{N}(x_{n}-\mu)^2$$
The Standard Deviation is the square root of the variance:
$$\sigma=\sqrt{\frac{1}{N}\sum\limits_{n=1}^{N}(x_{n}-\mu)^2}$$

#### 0.1.3 Normal Distribution
$$f(x;\mu,\sigma^{2})=\frac{1}{{\sqrt{2\pi\sigma^2}}}e^{\frac{-(x-\mu)^{2}}{2\sigma^{2}}}$$
### 0.1.4 Random Variable

A random variable describes the hidden state of the system. It is a set of possible values from a random experiment.

The random variable is described by the probability density function of the normal distribution and characterized by moments.

Moments of the random value are expected values of powers of the random Variable.
- The $k^{th}$ raw moment is the expected value of the $k^{th}$ power of the random variable: $E(X^{k})$ 
  (E(X) is the mean of the sequence of measurements)
- The $k^{th}$ central moment is the expected value of the $k^{th}$ power of the random variable distribution about its mean: $E((X-\mu_{X})^k)$
  (The second central moment is the variance of the sequence of measurements)

## 0.2 Two Dimensional Algebra and Stochastics
### 0.2.1 Expectation Algebra
Reminder : The expectation of the random variable $E(X)$ equals the mean of the random variable:
$$E(X)=\mu_{X}=\sum\limits xp(x)$$

>[!Rules]-
>![[Pasted image 20230629105731.png]]

### 0.2.2 Covariance Algebra
Reminer: The Variance is the squared standard deviation
$$\sigma^{2}=\frac{1}{N}\sum\limits_{n=1}^{N}(x_{n}-\mu)^2$$
>[!Rules]-
>![[Pasted image 20230629110043.png]]

### 0.2.3 Multivariate Covariance
#### 0.2.3.1 Covariance
Covariance is a measure of the strength of the correlation between two or more sets of random variates.
$$COV(X,Y)=\frac{1}{N}\sum\limits_{i=1}^{N}(x_{i}-\mu_{x})(y_{i}-\mu_{i})$$
$$=\frac{1}{N-1}\sum\limits_{i=1}^{N} (x_{i}y_{i})- \frac{N}{N-1}\mu_{x}\mu_{y}$$
If two data sets are uncorrelated the variance and mean of the measurements for one value do not depend on the measurement of the second value and vice versa. Visually this corresponds to a circular or horizontal/vertically oval shaped distribution of measurements.

For a zero-mean random variable the covariance equations becomes:
$$COV(X,Y)=\frac{1}{N-1}\sum\limits_{i=1}^{N} (x_{i}y_{i})$$

>[!Example]+
>$$x=[2,3,-1,4]^{T}$$
>$$y=[8,7,9,6]^{T}$$
>![[Pasted image 20230629141752.png]]
>$$COV=\frac{1}{N-1}x^{T}y- \frac{N}{N-1}\mu_{x}\mu_{y}=-2.67$$


#### 0.2.3.2 Covariance Matrix
The covariance Matrix is a square matrix that represents the covariance between each pair of elements in a given multivariate random variable.

e.g. in 2D:
$$\Sigma=\left[\begin{array}{c}
\sigma_{xx}&\sigma_{xy}\\
\sigma_{yx}&\sigma_{yy}
\end{array}\right]=
\left[\begin{array}{c}
\sigma^{2}_{x}&\sigma_{xy}\\
\sigma_{yx}&\sigma_{y}^{2}
\end{array}\right]=
\left[\begin{array}{c}
VAR(x)&COV(x,y)\\
COV(y,x)&VAR(y)
\end{array}\right]$$
$$COV(x,y)=COV(y,x)$$
The covariance matrix is positive semidefinite and its eigenvalues are non-negative (squared entries along the diagonal)

The Covariance Matrix of a vector (with itself) is given by:
$$COV(x)=E((x-\mu_{x})(x-\mu_x)^T)$$

### 0.2.4 Multivariate Normal Distribution
$$p(x|\mu,\sigma)=\frac{1}{\sqrt{2\pi \sigma^{2}}}e^{- \frac{(x-\mu)^{2}}{2\sigma^{2}}}=\mathcal{N}(\mu,\sigma^{2})$$
for a multidimensional (n-Dimensional) random variable the normal distribution is described by:
$$p(x|\mu,\Sigma)=\frac{1}{\sqrt{(2\pi)^{n}|\Sigma|}}e^{-\frac{1}{2}(x-\mu)^{T}\Sigma^{-1}(x-\mu)}$$



# 1 $\alpha-\beta-\gamma-$Filter
## 1.1 Static Model
First Idea is to take the measurements and build an average to get the right value
$$\hat{x}_{n,n}=\frac{1}{n}(z_{1}+z_{2}+...+z_{n})=\frac{1}{n}\sum\limits_{i=1}^{n}(z_i)$$
The dynamic model in this case is static so:
$$\hat{x}_{n+1,n}=\hat{x}_{n,n}$$
where the first index indicates that the variable is an estimate for a future time point and the second index tells at which time the estimation is made.

In order to make the equation more efficient the estimate should not be based on ALL previous measurements. Thus the idea is to estimate one step ahead based on only the last estimate:

$$\hat{x}_{n,n}=\frac{1}{n}\left(\sum\limits_{i=1}^{n-1}z_{i}+z_{n}\right)=\frac{1}{n}\sum\limits_{i=1}^{n-1}z_{i}+ \frac{1}{n}z_{n}$$
we can keep the second part as it only refers to the current measurement
For the first part we can use a trick to make it act as the previous estimate:
$$\frac{n-1}{n} \frac{1}{n-1}\sum\limits_{i=1}^{n-1}z_{i}=\frac{n-1}{n}\hat{x}_{n-1,n-1}=\hat{x}_{n-1,n-1}- \frac{1}{n}\hat{x}_{n-1,n-1}$$
Which gives us the current estimate based on the previous estimate and the current measurement:
$$\hat{x}_{n,n}=\hat{x}_{n-1,n-1}+ \frac{1}{n}(z_{n}-\hat{x}_{n-1,n-1})$$
We now don't want to base our estimation on the current measurement but rather find an estimate based on the last measurement. For this the ==dynamic equation== is used:
$$\hat{x}_{n,n-1}=\hat{x}_{n-1,n-1}$$
meaning that the expected behavior of the state is static. The value for the time n should not chance compared to the value at time n-1. Meaning that we can just replace it in the average equation

$$\hat{x}_{n,n}=\hat{x}_{n,n-1}+ \frac{1}{n}(z_{n}-\hat{x}_{n,n-1})$$
The above equation in its general form is called ==*the state update equation*==
$$\hat{x}_{n,n}=\hat{x}_{n,n-1}+ \alpha_{n}(z_{n}-\hat{x}_{n,n-1})$$
The $(z_{n}-\hat{x}_{n,n-1})$-part of the Term is called ==innovation==.

```Matlab
% Static Example
z1=[996, 994, 1021, 1000, 1002, 1010, 983, 971, 993, 1023]
xhat(1,1)=1000;
for n=2:11 %1:10 if 1->0
    xhat(n,n-1)=xhat(n-1,n-1);
    xhat(n,n)  =xhat(n,n-1)+1/n*(z1(n-1)-xhat(n,n-1));
end

estimates=diag(xhat)';
figure(1)
hold on
plot(estimates,'r')
plot(z1,'b')
plot([1 11],[1000 1000],'g')
hold off
```

## 1.2 Constant Velocity
The dynamic model now changes to:
$$\dot{x}=\frac{dx}{dt}=const.$$
meaning that:
$$x_{n}=x_{n-1}+\dot{x}\Delta t$$
$$\dot{x}_{n+1}=\dot{x}_{n}$$
Those two dynamic equations are called ==*State Extrapolation Equations*== / ==*Transition Equation*== or ==*Prediction Equation*==

We get the time interval and the current position as distance from a measurement point.
For the velocity we use an initial guess
Now we can calculate the estimate of the aircraft position one step ahead by the dynamical equations (==*prediction*==)
$$\hat{x}_{n,n-1}=\hat{x}_{n-1,n-1}+\Delta t \hat{\dot{x}}_{n-1,n-1}$$
Now we have the current *estimated* values of the states.

Now we use the *State Update Equation* to combine the measurements and predictions.
$$\hat{\dot{x}}_{n,n}=\hat{\dot{x}}_{n,n-1}+\beta\left( \frac{z_{n}-\hat{x}_{n,n-1}}{\Delta t} \right)$$
$$\hat{x}_{n,n}=\hat{x}_{n,n-1}+\alpha(z_{n}-\hat{x}_{n,n-1})$$

Those equation combine the estimates with the current measurement (hence the adaption for velocity as only position is measured)
The factors can be chosen based on how much I trust that measurements. A high value means I trust the measurement a lot, a low value means i trust the dynamic model a lot more.

```Matlab
%measurements (position)
z2=[30171, 30353, 30756, 30799, 31018, 31278, 31276, 31379, 31749, 32175]
dt=5;%s
alpha=0.8; %how much do I not trust my dynamic model
beta=0.5;  %how much do I not trust the static assumtion

%initial states
x2hat(1,1)=30000;
xd2hat(1,1)=40;
for n=1:length(z2)
    % position estimation and update (dynamic model)
    x2hat(n+1,n)=x2hat(n,n)+dt*xd2hat(n,n);
    x2hat(n+1,n+1)=x2hat(n+1,n)+alpha*(z2(n)-x2hat(n+1,n));
    
    % velocity estimation and update (static)
    xd2hat(n+1,n)=xd2hat(n,n);
    xd2hat(n+1,n+1)=xd2hat(n+1,n)+beta*(z2(n)-x2hat(n+1,n))/dt;
end

xestimates2=diag(x2hat(2:end,2:end))';
xpredict2=diag(x2hat,-1);
```

## 1.3 Acceleration in one Dimension
The dynamics now become:
$$\ddot{x}_{n}=\ddot{x}_{n-1}=const.$$
$$\dot{x}_{n}=\dot{x}_{n-1}+\ddot{x}_{n-1} \Delta t$$
$$x_{n}=x_{n-1}+\Delta t \dot{x}_{n-1}+ \frac{\Delta t^{2}}{2} \ddot{x}_{n-1}$$

Thus the *predictions* are as follows:
$$\hat{x}_{n,n-1}=x_{n-1,n-1}+\Delta t \hat{\dot{x}}_{n-1,n-1}+ \frac{\Delta t^{2}}{2} \hat{\ddot{x}}_{n-1,n-1}$$
$$\hat{\dot{x}}_{n,n-1}=\hat{\dot{x}}_{n-1,n-1}+ \Delta t \hat{\ddot{x}}_{n-1,n-1}$$
$$\hat{\ddot{x}}_{n,n-1}=\hat{\ddot{x}}_{n-1,n-1}$$
And the update works as follows:
$$\hat{x}_{n,n}=\hat{x}_{n,n-1}+\alpha(z_n-\hat{x}_{n,n-1})$$
$$\hat{\dot{x}}_{n,n}=\hat{\dot{x}}_{n,n-1}+\beta\left(\frac{z_n-\hat{x}_{n,n-1}}{\Delta t}\right)$$
$$\hat{\ddot{x}}_{n,n}=\hat{\ddot{x}}_{n,n-1}+\gamma\left(\frac{z_n-\hat{x}_{n,n-1}}{0.5\Delta t^2}\right)$$
```Matlab
z4=[30221 30453 30906 30999 31368 31978 32526 33379 34698 36275];
alpha=0.5;
beta=0.4;
gamma=0.1;

%initial guess
x4hat(1,1)=30000;
v4hat(1,1)=50;
a4hat(1,1)=0;

for n=1:length(z2)
    %State Estimation and update for position
    x4hat(n+1,n)=x4hat(n,n)+dt*v4hat(n,n)+(dt^2)/2*a4hat(n,n);
    x4hat(n+1,n+1)=x4hat(n+1,n)+alpha*(z4(n)-x4hat(n+1,n));
    
    % velocity estimation and update
    v4hat(n+1,n)=v4hat(n,n)+dt*a4hat(n,n);
    v4hat(n+1,n+1)=v4hat(n+1,n)+beta*(z4(n)-x4hat(n+1,n))/dt;

    % acceleration estimation and update
    a4hat(n+1,n)=a4hat(n,n);
    a4hat(n+1,n+1)=a4hat(n+1,n)+gamma*(z4(n)-x4hat(n+1,n))/(0.5*dt^2);
end
xestimates4=diag(x4hat(2:end,2:end))';
xpredict4=diag(x4hat,-1);

vestimates4=diag(v4hat(2:end,2:end))';
vpredict4=diag(v4hat,-1);

aestimates4=diag(a4hat(2:end,2:end))';
apredict4=diag(a4hat,-1);
```

# 2  Kalman Filter
## 2.1 One Dimensional Kalman Filter Without Process Noise
The Kalman Filter treats the estimate as a random variable and thus not only estimates a state but also extrapolates the variance of that estimation ($p_{n,n}$).

The variance extrapolation is also a prediction and is based on the dynamic model of the System.

>[!Attention]+
>For a random Variable $X$ with variance $\sigma$, $kX$ is distributed normally with $k^2\sigma^2$
>e.g.
>For the case of constant velocity:
>$$p_{n,n-1}^v=p_{n-1,n-1}^v$$
>$$p_{n,n-1}^{x}=p_{n-1,n-1}^{x}+\Delta t^{2}\cdot p_{n-1,n-1}^{v}$$
>where the $\Delta t$ part gets squared

This is the ==*Covariance Extrapolation Equation*==

Now there is two predictions: The Covariance and the State Prediction.
**To update the predictions made at the last state with the current measurement to provide the current state estimate the Kalman Filter uses a combination of measurement and prediction that minimizes the uncertanty for that estimation.**

### 2.1.1 The Update Process
The current state estimate is a wighted mean of the measurement and the prior state estimate
$$\hat{x}_{n,n}=w_{1}z_{n}+w_{2}\hat{x}_{n,n-1}$$
$$w_{1}+w_{2}=1$$
resulting in:
$$\hat{x}_{n,n}=w_{1}z_{n}+(1-w_{1})\hat{x}_{n,n-1}$$
$$p_{n,n}=w_{1}^{2}r_{n}+(1-w_{1})^{2}p_{n,n-1}$$
where $r_{n}$ is the variance of the measurement $z_{n}$.

Since the state estimate should be optimal is is necessary to minimize $p_{n,n}$. 
$$\frac{dp_{n,n}}{dw_{1}}=2w_{1}r_{n}-2(1-w_{1})p_{n,n-1}=0$$
this gives us the point where the slope of $p_{n,n}$ is zero -> ?which apperently is a minimum?

>[!Question]
>Couldn't this also be a maximum?

This gives us the ==*Kalman Gain Equation*==
$$w_{1}=K_{n}=\frac{p_{n,n-1}}{r_{n}+p_{n,n-1}}$$
which gives a number between zero and one.

inserting this in the update equation of the variance $p_{n,n}$ we can derive a simpler form of it using the Kalman Gain

$$p_{n,n}=(1-K_{n})p_{n,n-1}$$
Note that in this ==*Covariance Update Equation*== the current measurement variance is still represented within $K_{n}$.

### 2.1.2 The Process
*Initialization (n=0) / Estimation(n>0)*
$$\hat{x}_{n,n}/p_{n,n}$$
**Step1: Predict with dynamic model**
>[!Note]+ e.g.: constant velocity system
>$$\hat{x}_{n+1,n}=\hat{x}_{n,n}+\Delta t \hat{\dot{x}}_{n,n}$$
>$$\hat{\dot{x}}_{n+1,n}=\hat{\dot{x}}_{n,n}$$

Results in *Prediction*:
$$\hat{x}_{n+1,n} / p_{n+1,n}$$
**Step 2: Update**
!Note that there is a time step between the prediction and the update, thus:
$$\hat{x}_{n+1,n}\rightarrow \hat{x}_{n,n-1}\ \wedge\ p_{n+1,n} \rightarrow p_{n,n-1}$$
>[!Note]+ Update Equations
>$$\hat{x}_{n,n}=\hat{x}_{n,n-1}+K_{n}(z_{n}-\hat{x}_{n,n-1})$$
>$$p_{n,n}=(1-K_{n})p_{n,n-1}$$
>$$K_{n}=\frac{p_{n,n-1}}{p_{n,n-1}+r_{n}}$$

Results in *Estimation*:
$$\hat{x}_{n,n}/p_{n,n}$$
From here it circles back to Step 1...

![[Pasted image 20230628110508.png]]

### 2.1.3 Kalman Gain Intuition
$$K_{n}=\frac{p_{n,n-1}}{p_{n,n-1}+r_{n}}$$
-  A low Kalman Gain:
  If the uncertainty (variance) of the measurement is high compared to the uncertainty of the prediction this would result in a low Kalman Gain.
  This would result in the estimates being really close to the prediction in every time step.
- A high Kalman Gain:
  If the uncertainty of the prediction is higher than the one of the measurement this results in a high Kalman Gain.
  A high Kalman Gain means, that the estimates would be close to the measurement in every time step

## 2.2 Adding Process Noise

Adding process noise changes the *Covariance Prediction Equation*
$$p_{n+1,n}=dynamic\ eq. +\ q$$
where $q$ is the variance of the process.

Whith the implementation of process noise a dynamic model that isn't well fitted for the process can be compensated to a certain amount. The best Kalman Filter however is still one that involves a model that is as close to reality as possible.

>[! Example]- Compensation of bad fittet Model with process noise
>In this Example a steady model is used to estimate the temperature of a heating liquid in a tank. It is assumed that the process has a small variance of about $q=0.0001$
>![[Pasted image 20230628164324.png]]
>With an adaption of the assumed process noise to $q=0.15$ the estimation can be improved without changing the dynamic model
>![[Pasted image 20230628164613.png]]





## 2.3 Multivariate Kalman Filter
We assume a Linear Kalman Filter (LKF). Meaning that we assume the System Dynamics to be linear.

For the Multivariate Kalman Filter the System States are no longer one dimensional.
E.g. the position, velocity and acceleration of an airplane is nine-dimensional
$$\left[\begin{array}{c}
x&y&z&\dot{x}&\dot{y}&\dot{z}&\ddot{x}&\ddot{y}&\ddot{z}
\end{array}\right]^T$$
Assuming constant acceleration, we can describe the system dynamics by nine motion equations:
$$\left\{\begin{array}{l}
x_{n}=x_{n-1}+\dot{x}_{n-1}\cdot \Delta t + \frac{1}{2}\ddot{x}_{n-1}\cdot \Delta t^2\\
y_{n}=y_{n-1}+\dot{y}_{n-1}\cdot \Delta t + \frac{1}{2}\ddot{y}_{n-1}\cdot \Delta t^2\\
z_{n}=z_{n-1}+\dot{z}_{n-1}\cdot \Delta t + \frac{1}{2}\ddot{z}_{n-1}\cdot \Delta t^2\\
\dot{x}_{n}=\dot{x}_{n-1}+\ddot{x}_{n-1}\cdot \Delta t\\
\dot{y}_{n}=\dot{y}_{n-1}+\ddot{y}_{n-1}\cdot \Delta t\\
\dot{z}_{n}=\dot{z}_{n-1}+\ddot{z}_{n-1}\cdot \Delta t\\
\ddot{x}_{n}=\ddot{x}_{n-1}\\
\ddot{y}_{n}=\ddot{y}_{n-1}\\
\ddot{z}_{n}=\ddot{z}_{n-1}
\end{array}\right\}$$

### 2.3.1 State Extrapolation Equation (Prediction)
$$\hat{x}_{n+1,n}=F\hat{x}_{n,n}+Gu_{n}+w_{n}$$
where $u_{n}$ is a control or input variable and $w_{n}$ is a process noise
The System Dynamics are written as a set of first order differential equations (discrete form)
$$\dot{x}(t)=Ax(t)+Bu(t)$$
$$x(t+\Delta t)=e^{A\Delta t}x(t)+\int_{0}^{\Delta t}e^{At}dt \cdot Bu(t)=Fx(t)+Gu(t)$$
### 2.3.2 Covariance Extrapolation Equation (Prediction)
$$P_{n+1,n}=FP_{n,n}F^{T}+Q$$
where $Q$ is the process noise matrix (It's effects on the Estimation are as described in the one dimensional case)

### 2.3.3 Measurement
$$z_{n}=Hx_{n}+v_{n}$$
where $H$ is an observation matrix and $v_{n}$ is a random noise vector
Sometimes only some states are measurable and for the other ones a combination of the measurable states can be used

### 2.3.4 Measurement Uncertainty (Definition)
$$R_{n}=E(v_{n}v_{n}^T)$$
### 2.3.5 Process Noise Uncertainty (Definition)
$$Q_{n}=E(w_nw_{n}^T)$$
### 2.3.6 Estimation Uncertainty (Definition)
$$P_{n,n}=E(e_{n}e_{n}^{T})=E((x_n-\hat{x}_{n,n})(x_{n}-\hat{x}_{n,n})^{T})$$
### 2.3.7 State Update Equation
$$\hat{x}_{n,n}=\hat{x}_{n,n-1}+K_{n}(z_{n}-H\hat{x}_{n,n-1})$$
where $(z_{n}-H\hat{x}_{n,n-1})$ is called the ==innovation==

### 2.3.8 Covariance Update Equation
$$P_{n,n}=(I-K_{n}H)P_{n,n-1}(I-K_{n}H)^{T}+K_{n}R_{n}K_{n}^{T}$$
with Kalman Gain $K_{n}$

### 2.3.9 The Kalman Gain Equation
$$K_{n}=P_{n,n-1}H^{T}(HP_{n,n-1}H^{T}+R_{n})^{-1}$$

# 3 Non Linear Kalman Filter
The Kalman Filter algorithm assumes that the distribution of all random variables is Gaussian. For non-linear systems, this assumption does not hold anymore.
>[!Note]+ Example: Pendulum
>$$F=-mg\sin(\theta)$$
>$$v=\frac{ds}{dt}=L \frac{d\theta}{dt}$$
>$$(s=L\theta)$$
>$$L \frac{d^{2}\theta}{dt^{2}}=-g\sin(\theta)$$
>
>$$\hat{\theta}_{n+1,n}=\hat{\theta}_{n,n}+\hat{\dot{\theta}}_{n,n}\Delta t$$
>$$\hat{\dot{\theta}}_{n+1,n}=\hat{\dot{\theta}}_{n,n}+\hat{\ddot{\theta}}_{n,n}\Delta t = \hat{\dot{\theta}}_{n,n}- \frac{g}{L} \sin(\hat{\theta}_{n,n})\Delta t$$
>
>$$f(\hat{x}_{n+1,n})=\left[\begin{array}{l}
>\hat{\theta}_{n,n}+\hat{\dot{\theta}}_{n,n}\Delta t\\\hat{\dot{\theta}}_{n,n}- \frac{g}{L} \sin(\hat{\theta}_{n,n})\Delta t\end{array}\right]$$







