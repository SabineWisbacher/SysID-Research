---
aliases: []
---
## Start Date: 2023-04-26

> Category: Note

Tags:
#ControlBasics 

Links:


>[! Summary]
>If the system keeps moving as long as I give an input (IT1) a simple P controller would be generally sufficient. If the System comes to a knew steady point for a constant input (PT1) an integration gain is needed in the controller. If the System has a lot of inertia (so it overshoots and comes back to a new steady condition) a derivative gain is needed to provide damping.


---
## PT1-System
$$\frac{1}{s+1}$$
![[Pasted image 20230426155837.png]]

## IT1-System
$$\frac{1}{s^{2}+s}$$
![[Pasted image 20230426155926.png]]

## DT1-System
$$\frac{s}{s+1}$$
![[Pasted image 20230426160153.png]]