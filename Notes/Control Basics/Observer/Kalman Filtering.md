---
aliases: []
---
## Start Date: 2023-06-26

> Category: Note

Tags:
#Observer #KalmanFilter 
#ControlBasics

Links:
https://www.kalmanfilter.net/background.html
[[@(becker2023)_Kalman Filter from the Ground Up]]([[becker2023.pdf]])

>[! Summary]
>

---


# Tutorial: Linear Kalman Filter
[[@(becker2023)_Kalman Filter from the Ground Up|becker2023]]
## 1) State and Covariance Prediction
$$\hat{x}_{n+1,n}=F\hat{x}_{n,n}+Gu_{n}+w_{n}$$
$$P_{n+1,n}=FP_{n,n}F^{T}+Q$$
>[!Definition]+
>$F$ - System Dynamics (1st Order Differential Eq.)
>$G$ - Input Transition Matrix (measurable control input)
>$Q$ - Covariance Matrix
>			For a non-controlled system: $Q=FQ_{a}F^T$
>			$Q_{a}$ in this case represents a matrix that gives where the process noise occurs
>			For a controlled System: $Q=G\sigma_{a}^{2}G^T$

## 2) Measurement and Kalman Gain
$$z_{n}=Hx_{n}+v_{n}$$
$$K_{n}=P_{n,n-1}H^T(HP_{n,n-1}H^T+R_{n})^{-1}$$

>[!Definition]+
>$H$ - Observation Matrix
>$R$ - Measurement noise covariance matrix

## 3) Update Estimates
$$\hat{x}_{n,n}=\hat{x}_{n,n-1}+K_{n}(z_{n}-H\hat{x}_{n,n-1})$$
$$P_{n,n}=(I-K_{n}H)P_{n,n-1}(I-K_{n}H)^{T}+K_{n}R_{n}K_{n}^{T}$$





