## Start Date: 2022-12-14

> Category: Note

Tags:
 #LTI
 #ControlBasics 

Links:
[[@(verhaegen2014)_Subspace Techniques in System Identification|verhaegen2014]]
[[@(qin2006)_An overview of subspace identification|qin2006]]

>[! Summary]
>

---
## The Identification Problem (LTI)

While **ST** formulates an *intermediate step* in deriving the parameters of the system matrices from the given data (input/output), the **parametric model identification** framework aims for a direct estimation of the parameters of the system matrices.

The parametric model identification framework usually uses ==nonlinear parameter optimization techniques== for this.

The *intermediate step* and the subsequent derivation of the system matrices in ST are done via ==convex optimization methods== and/or ==linear algebra methods==.

The state space model is can be described in different forms:

### Process Form:
$$x_{k+1}=Ax_{k}+Bu_{k}+w_{k}$$$$y_{k}=Cx_{k}+Du_{k}+v_{k}$$
$x_{k}$ - state vector,
$u_{k}$ - measurable input,
$y_{k}$ - measurable output,
$w_{k}$ - state noise,
$v_{k}$ - output measurment noise 

### Innovation Form:
with the Kalman Gain $K$ and the innovations of the Kalman filter $e_{k}$
$\hat{x}_{k+1}=A\hat{x}_{k}+Bu_{k}+K(y_{k}-C\hat{x}_{k}-Du_{k})$
$e_{k}=y_{k}-C\hat{x}_{k}-Du_{k}$

$$x_{k+1}=Ax_{k}+Bu_{k}+Ke_{k}$$
$$y_{k}=Cx_{k}+Du_{k}+e_{k}$$
Here the innovation $e_{k}$ is white noise that is independent of past input and output data.

### Predictor Form:
$$x_{k+1}=A_{K}x_{k}+B_{K}z_{k}$$
$$y_k=Cx_{k}+Du_{k}+e_{k}$$

$z_{k}=[u_{k}^{T},\ y_{k}^{T}]^{T}$
$A_{K}=A-KC$
$B_{K}=[B-KD,\ K]$


#### The z-Transform
[The Mathematics of Signal Processing | The z-transform, discrete signals, and more - YouTube](https://www.youtube.com/watch?v=hewTwm5P0Gg)





