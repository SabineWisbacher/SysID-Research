---
aliases: []
---
## Start Date: 2023-02-23

> Category: Note

Tags: #numerik 

Links:
https://www.kalmanfilter.net/background.html


>[! Summary]
>Stochastics and Signal Processing are tightly connected through entities as variance, standard deviation, normal distribution, estimate, accuracy, precision, mean, expected value and random variables.

---
# Mean and Expected Value

If the considered Value is not hidden (no measurement noise) then the overall outcome over a number of experiments is the mean value:
$$V_{mean}= \frac{1}{N} \sum\limits_{n=1}^{N}V_n(=\mu)$$

The expected Value is the Value you would expect your hidden variable to have over a long time or many experiments.
$$W= \frac{1}{N}\sum\limits_{n=1}^{N}W_{n}(=E)$$

# Variance and Standard Deviation
Variance is the average value of all squared distances from the mean
$$\sigma^2=\frac{1}{N}\sum\limits_{n=1}^{N}(x_{n}-\mu )^2$$
For an estimated mean the equation is slightly adapted
$$\sigma^2=\frac{1}{N-1}\sum\limits_{n=1}^{N}(x_{n}-\mu )^2$$
The factor $N-1$ is called Bessel's correction.

Standart deviation (the mean of the absolut deviation of all measurements from the mean value)
$$\sigma=\sqrt{\frac{1}{N}\sum\limits_{n=1}^{N}(x_{n}-\mu )^2}$$

# Normal Distribution
Probability is centered around a mean value.

The more options there are for height, the less likely any specifiy measurement will be one of them. Thus the wider the curve gets, the lower the maximum will be

The normal probability density function (pdf) is
$$y=f(x|\mu,\sigma)=\frac{1}{\sigma \sqrt{2\pi}}e^{\frac{-(x-\mu)^{2}}{2\sigma^{2}}},for \ x\in \mathbb{R}$$
https://www.youtube.com/watch?v=oI3hZJqXJuc&list=PLblh5JKOoLUJUNlfvCNhJMNjNNpt5ljcR&index=2

The covariance is:
$$V=\frac{1}{N-1}\sum\limits_{i=1}^{N}|A_{i}-\mu|^2$$
with the mean value $\mu$ beeing
$$\mu=\frac{1}{N}\sum\limits_{i=1}^{N}A_i$$
# Random Variables
A random variable describes the hidden state of the system. A random variable is a set of possible values from a random experiment.

$E(X)$ is the mean of the sequence of measurements (Expected Value of the hidden states)
$E((X-\mu_{X})^2)$ is the variance of the sequence of measurements.

# Estimate, Accuracy and Precision
![[Pasted image 20230328125602.png]]
Accuracy indicates how close the measurement is to the true value. Low-accuracy systems are called biased systems since their measurements have a built-in systematic error (bias).

Precision describes the variability in a series of measurements of the same parameter. High-precision systems have low variance in their measurements (i.e., low uncertainty), while low-precision systems have high variance in their measurements (i.e., high uncertainty). The random measurement error produces the variance.