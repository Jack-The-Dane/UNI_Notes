The discrete design method relies on a discretized plant model. The discrete transfer
function of a system $G(s)$ and preceding zero-order hold is
![[Pasted image 20240405094241.png]]
where $Z$ denotes the z-transformation.
Subsequent to the discretization, the control system can be analyzed based on the
closed-loop transfer function
![[Pasted image 20240405094317.png]]
Since the structure of the continuous and discrete closed-loop transfer functions are the
same, the stability of the system can be studied via the characteristic equation
$$1 + K(z)G(z) = 0$$
Consequently, the controller K(z) can be designed via root locus or any of the other
methods.

## Design procedure
![[Pasted image 20240405094421.png]]
