## Introduction
Real electromechanical systems have saturations on their physical variables. In particular,
the output of any actuator is limited from above and below.
![[Pasted image 20240405082429.png]]
The saturation of actuators must be taken into account, when integral action is present in
the controller. Otherwise, the performance of the system may degrade significantly.
![[Pasted image 20240405082505.png]]
If a setpoint is given to the system that cannot be reached, then the integrator winds up,
and a delay is experienced when changing the setpoint value.
![[Pasted image 20240405082932.png]]
It is important to only give a system reachable references.

## Overview
There are 2 methods of anti-windup:
- Back-Calculation
- Conditional integration (best and easiest)

Both methods utilize the following signal:
![[Pasted image 20240405083144.png]]

## Back-Calculation
The anti-windup scheme called back-calculation recomputes the integral term when the
system input is saturated, as shown below.
![[Pasted image 20240405083256.png]]
The value of the integrator output is not changed instantaneously, but it is changed based
on the tracking time constant $T_t$. 
This construction will, when v is larger than u, subtract a value of $e_s$ from the integrator input before it is integrated.
### Input and output of integrator
![[Pasted image 20240405083752.png]]
This means that $e_s$ is proportional to the error, and the error never reaches zero, because $e_s$ is not zero in steady-state. 
![[Pasted image 20240405084049.png]]
### Performance
![[Pasted image 20240405084131.png]]

## Conditional integration
The anti-windup scheme called conditional integration (also known as clamping) is a bit simpler, and just stops integrating, when the system is in saturation.
![[Pasted image 20240405084434.png]]
Although conditional integration is simpler than back-calculation, it also improves the performance of the system.
![[Pasted image 20240405084500.png]]
