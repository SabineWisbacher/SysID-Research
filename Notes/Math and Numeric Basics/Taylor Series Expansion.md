---
aliases: [Taylor Series]
---
## Start Date: 2023-03-07

> Category: Note

Tags:
#numerik 

Links:


>[! Summary]
>Taylor Series Expansions are polynomial approximations of functions
>
>$$P(x)=f(a)+ \frac{df}{dx}(a) \frac{(x-a)^{1}}{1!}+ \frac{d^{2}f}{dx^{2}}(a) \frac{(x-a)^{2}}{2!}...$$

---

The number of degrees of Freedom depends on the order of polynomia that is used to define the function. The Idea is to match every polynomia coefficient to a characteristic of the function.
$$p(x)=c_{0}+c_{1}x+c_{2}x^2+c_{3}x^{3}+c_{4}x^{4}...$$
$$\frac{d}{dx}p(x)=c_{1}+ 2c_{2}x+ 3c_{3}x^{2}+ 4c_{4}x^{3}...$$
$$\frac{d^{2}}{dx^{2}}p(x)= 2c_{2}+ 6c_{3}x+ 12c_{4}x^{2}...$$
$$\frac{d^{3}}{dx^{3}}p(x)= 6c_{3}+ 24c_{4}x...$$
$$\frac{d^4}{dx^4}p(x)=24c_4...$$
$$P(x)=f(x)+\frac{d}{dx}f(x) \cdot x+ \frac{1}{2} \frac{d^{2}}{dx^{2}}f(x)\cdot x^2+\frac{1}{2\cdot 3} \frac{d^{3}}{dx^{3}}f(x)\cdot x^3...$$

![[Pasted image 20230307133524.png]]
In some cases the order is fixed (the derivatives of the function at the operating point are zero at some point).
For sin or cos functions (or any periodic function i guess) it depends on the number of polynomias you want to use (at some point the solution will not get a lot better with more polynomials)
![[Pasted image 20230307140136.png]]

The Taylor Series Expansion can be used for a linearization around an operating point. (As the first and second term represents the value of an operating point and the slope of the function at that point). This becomes more interessting for functions with multiple variables:

If $f(\cdot)$ is a function of $x$ and $y$, and operated near the operating point $[x,y]=[a,b]$:

$$f(x,y)\approx f(a,b)+ \frac{\delta}{\delta x}f(a,b)(x-a)+ \frac{\delta}{\delta y}f(a,b)(y-b)+ ...$$$$...\frac{1}{2} \left(A(x-a)^2+2B(x-a)(y-b)+C(y-b)^2\right)$$
with:
$$A=\frac{\delta^2}{\delta x^{2}}f(a,b)$$
$$B=\frac{\delta^2}{\delta x \delta y}f(a,b)=\frac{\delta^2}{\delta y \delta x}f(a,b)$$
$$C=\frac{\delta^2}{\delta y^{2}}f(a,b)$$
