![[Pasted image 20240216100237.png]]
![[Pasted image 20240216100523.png]]
![[Pasted image 20240216100551.png]]
(Cascade is the red one)
![[Pasted image 20240216100635.png]]
$C_s(s)$ is the secondary controller
## Design
Cascade control can be used when
- There should be a well defined relation between the primary and secondary
measured variable
- Essential disturbances should act in the inner loop
- The inner loop should be faster than the outer loop. A rule of thumb is that the
average residence times should have a ratio of at least five.
- should be possible to have a high gain in the inner loop.
--------
The following procedure should be followed to tune a cascade control
1. Tune inner-loop controller (Cs) such that the transfer function from u′ to ys is critically
damped or over damped (unity DC gain is not a requirement).
2. Tune the outer-loop controller (Cp) such that the desired performance is obtained.

## DC Motor Control
![[Pasted image 20240216101713.png]]
![[Pasted image 20240216101728.png]]
![[Pasted image 20240216101749.png]]
