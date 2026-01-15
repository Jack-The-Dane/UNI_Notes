Lag Compensation: Approximates the PI control, i.e., it improves the steady state
tracking.
![[Pasted image 20240322093628.png]]
If z > p, then D(s) is called a lag compensation.

## Definition
![[Pasted image 20240322095457.png]]
![[Pasted image 20240322095516.png]]

## Design procedure
1. Determine open-loop gain K that will meet the phase margin requirement without
compensation.
2. Draw the Bode plot of the uncompensated system with crossover frequency from
Step 1, and evaluate the low-frequency gain.
3. Determine α to meet the low-frequency gain error requirement.
4. Choose the corner frequency $ω = 1/T$ (the zero of the lag compensator) to be one
decade below the crossover frequency $ω_c$.
5. The other corner frequency (the pole location of the lag compensator) is $ω = 1/αT$
6. Iterate on the design. Adjust compensator parameters (poles, zeros, and gain) until
all specifications are met.