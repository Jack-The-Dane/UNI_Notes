Emulation: Design continuous controller $K(s)$ and approximate it with $K(z)$ obtained via e.g. Tustin’s method.
The sampling frequency used for the discrete controller should be about 20 times the closed-loop bandwidth. Otherwise, special care should be takes in the design of the discrete controller.

## Emulating a PID-controller
![[Pasted image 20240405091129.png]]
$$u(t) = u_P + u_I + u_D$$
Each of the terms in the PID Controller is computed for discrete times in the following
### Proportional and integral terms
![[Pasted image 20240405091306.png]]
### Derivative term
![[Pasted image 20240405091428.png]]
### Discretization
![[Pasted image 20240405092037.png]]
![[Pasted image 20240405092216.png]]
## Design procedure
![[Pasted image 20240405093510.png]]
