---
aliases: [prediction based]
---
## Start Date: 2023-06-19

> Category: Note

Tags:
#SubspaceIdentification #LTI

Links:

[[@(vanoverschee1994)_N4SID_ Subspace algorithms for the identification of combined deterministic-stochastic systems]]([[vanoverschee1994.pdf]])

[[@(qin2006)_An overview of subspace identification]]([[qin2006.pdf]])


>[! Summary]
>

---
# PBSID Theory

## Basic Equations
The identification with PBSID is based on the system and an observer Equation.
The system equations are:

$$x_{k+1}=Ax_{k}+Bu_{k}+w_{k}$$
$$y_{k}=Cx_{k} +Du_{k}+v_{k}$$
The observer equations (in predictor form) are:
$$\hat{x}_{k+1}=A_{K}\hat{x}_{k}+B_{K}z_{k}$$
$$y_{k}=Cx_{k}+Du_{k}+e_{k}$$
with $z_{k}=[u_{k}^{T}, y_{k}^{T}]^{T}$ , $A_{K}=A-KC$ , $B_{K}=[B-KD,K]$ 

>[!sketch]-
>[[Drawing 2024-03-05 14.52.29.excalidraw]]



## Data Equation
$$Y_{f}=\Gamma_{f}X_{k}+H_{f}U_{f}+G_{f}E_{f}$$
using $$\hat{X}_{k}=\bar{L}_{p}Z_{p}+A_{K}^{p}X_{k-p}$$
under the assumtion that the influence of the initial condition has close to zero influence if we look back far enough, meaning that
$$\hat{X}_{k}=\bar{L}_{p}Z_{p}$$
we can insert that into the Data Equation
$$Y_{f}=\Gamma_{f}\bar{L}_{p}Z_{p}+H_{f}U_{f}+G_{f}E_{f}$$
$$Y_{f}=H_{fp}Z_{p}+H_{f}U_{f}+G_{f}E_{f}$$
with $H_{fp}$ beeing the combination of the extended observaibility matrix of the System and the controlability matrix from the observer.

## Estimation of A and C from $\Gamma_f$ 
With the nullspace of U
$$\Pi_{U}^{\perp}=I-\Pi_{U}=I-U^{T}(UU^{T})^{-1}U$$
and the assumtion that $Z_{p}$ is uncorrelated to $E_{f}$ (neither input nor output is connected to the output error)
==With this way of calculating the nullspace it has the same dimensions than U, which enables the following calculations but leads to errors as it doesn't have full rank.==


>[! Note]-
>Uncorrelated in terms of linear algebra means that the subspaces that the data forms are perpendicualar to each other (no datapoint of the one matrix can be reached trough any projection of the other matrices data points)
>
>Thus the scalar product of the two matrices is zero

the data equation reduces to:
$$Y_{f}\Pi_{U_{f}}^{\perp}Z_{p}^{T}=H_{fp}Z_{p}\Pi_{U}^{\perp}Z_{p}^{T}$$
The Matrix $\Gamma_{f}$ that we are looking for is embedded in $H_{fp}$ 
$$H_{fp}=Y_{f}\Pi_{U}^{\perp}Z_{p}^{T}\cdot (Z_{p}\Pi_{U}^{\perp}Z_{p}^T )^{-1}$$
