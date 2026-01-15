Lead Compensation: Approximates the PD control, i.e., it lowers the rise time and
decreases the overshoot.
![[Pasted image 20240322093615.png]]
If z < p, then D(s) is called a lead compensation
## Definition
The transfer function D(s) has a zero followed by a pole, and acts as a filtered PD
controller, when used as a feedback controller.
![[Pasted image 20240322094026.png]]
![[Pasted image 20240322094111.png]]
## Parameters
![[Pasted image 20240322094145.png]]
## Design procedure
1. Determine open-loop gain K to satisfy error or bandwidth requirements:
	1.1 To meet error requirement, pick K to satisfy error constants (Kp, KV , Ka) so that ess error
	specification is met.
	1.2 Alternatively, to meet bandwidth requirement, pick K so that the open-loop crossover
	frequency is a factor of two below the desired closed-loop bandwidth.
2. Evaluate the phase margin of the uncompensated system using the value K obtained
	from Step 1.
3. Allow for extra margin (about 10◦), and determine the needed phase lead φmax (one
	lead compensation should contribute a maximum of 60◦ to the phase).
4. Determine α from:
$$\alpha = \frac{1-\sin(\phi_{max})}{1+\sin(\phi_{max})}$$
![[Pasted image 20240322094426.png]]
5. Pick $ω_{max}$ to be the crossover frequency; thus, the zero is at $1/T = ω_{max} √α$ and the
pole is at $1/αT = ω_{max}/√α$.
6. Draw the compensated frequency response and check the phase margin.
7. Iterate on the design. Adjust compensator parameters (poles, zeros, and gain) until
all specifications are met.