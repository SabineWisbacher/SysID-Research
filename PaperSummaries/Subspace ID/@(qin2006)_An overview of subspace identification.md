---
aliases: [qin2006]
---

### S. Joe Qin(2006)

>Category: Paper
>[PDF](qin2006.pdf)
>[Zotero-Link](zotero://select/items/@qin2006)

>[!ABSTRACT]-
>

---

### Tags:

#CatA 

#SubspaceIdentification #LTI #n4sid

---
### References:


---
# N4SID

The system is written in ==process form==
$$x_{k+1}=Ax_{k}+Bu_{k}+w_{k}$$
$$y_{k}=Cx_{k}+Du_k+v_k$$
The observer (Kalman Filter) is written either in ==innovation form==
$$x_{k+1}=Ax_{k}+Bu_{k}+Ke_{k}$$
$$y_{k}=Cx_{k}+Du_{k}+e_{k}$$
or in ==predictor form==
$$x_{k+1}=A_{K}x_{k}+B_{K}z_{k}$$
$$y_{k}=Cx_{k}+Du_{k}+e_{k}$$
with: $z_{k}=[u_{k}^{T},y_{k}^{T}]^{T}$ , $A_{K}=A-KC$ and $B_{K}=[B-KD,K]$ 

>[! Note]- Derivation of Predictor Form
>see Notebook

For the prediction the equation can be iterated as follows:
$$\bar{L}_{p}=\left[\begin{array}{c}
B_{k}&A_KB_{K}&\dots&A_{K}^{p-1}B_{K}
\end{array}\right]$$
$$z_{p}(k)=\left[\begin{array}{c}
z_{k-1}^{T}&z_{k-2}^{T} &\dots& z_{k-p}^T 
\end{array}\right]^T$$
$$x_{k}=\bar{L}_{p}z_{p}(k)+A_{K}^{p}x_{k-p}$$
if $A_{K}$ is strictly stable this reduces to:
$$x_{k}=\bar{L}_{p}z_{p}(k)$$
Expanded to all sequences:
$$X_{k}=\bar{L}_{p}Z_{p}$$

This inserted in the data equation resulting from the system description:
$$Y_{f}=\Gamma_{f}X_{k}+H_{f}U_{f}+G_{f}E_{f}$$
$$Y_{f}=\Gamma_{f}\bar{L}_{p}Z_{p}+H_{f}U_{f}+G_{f}E_{f}$$
Defining $H_{fp}=\Gamma_{f}\bar{L}_{p}$

Now using the orthogonal complement $\Pi_{Uf}^{\perp}$ of $U_{f}$ and defining the process noise $E_{f}$ as uncorrelated to $Z_{p}$ ($E_{f}Z_{p}^{T}=0$)we get:

$$Y_{f}\Pi_{Uf}^{\perp}Z_{p}^{T}=H_{fp}Z_{p}\Pi_{Uf}^{\perp}Z_{p}^{T}$$
$$H_{fp}=Y_{f}\Pi_{Uf}^{\perp}Z_{p}^{T}\cdot(Z_{p}\Pi_{Uf}^{\perp}Z_{p}^{T})^{-1}$$

Now N4SID performes SVD on $H_{fp}Z_{p}$

$$H_{fp}Z_{p}=\hat{\Gamma_{f}\bar{L}_{p}}Z_{p}=USV^{T}\approx U_{n}S_{n}V_{n}^{T}$$
Defining $\hat{\Gamma}_{f}=U_{n}S_{n}^{\frac{1}{2}}$

