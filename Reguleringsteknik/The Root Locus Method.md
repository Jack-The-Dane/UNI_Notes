The root locus method is used for describing how the poles of G(s) move around in the
s-plane, when the parameter K changes. This can then be used for tuning the controller. K is the gain of the controller.

The root locus method can be used for describing how the closed-loop poles move in
the s-plane, when a controller gain is changed.

![[Pasted image 20240301082042.png]]
The roots of a system will move from **open-loop** poles to either **open-loop** zeroes or to infinity.

## Sensitivity to parameter variations
This method is resistant to errors due to parameter variations, as you can also examine how the poles move when you vary one or more of the parameters from 0 to infnity.

## Formula of PID controller
$$K(s) = k_p(1+T_ds + \frac{1}{T_is}) = k_p \frac{t_ds² + s+ \frac{1}{T_i}}{s}$$
It is not possible to choose the location of your pole, only the zeroes.

## Problem formulation
![[Pasted image 20240301083418.png]]
Where K is the parameter you want to change. to observe the change in the system. G(s) is the rest of the system. It is important that K is isolated.
## Examples
![[Pasted image 20240301083704.png]]
Here the pole will be at $-1\over \tau$ if K is 0, and move towards -infinity as K increases.

![[Pasted image 20240301084103.png]]
![[Pasted image 20240301084114.png]]

# Root Locus
## Notation
![[Pasted image 20240301091154.png]]
## Example
![[Pasted image 20240301091227.png]]
![[Pasted image 20240301091249.png]]

## Rules
![[Pasted image 20240301091627.png]]
![[Pasted image 20240301091756.png]]
**Rule 3: When roots are complex they occur in conjugate pairs**
![[Pasted image 20240301092344.png]]
So between the first and second pole, the third and fourth and so on, when going from right to left.
![[Pasted image 20240301092838.png]]
### Rule 6
![[Pasted image 20240301093148.png]]
This is used for calculating how many lines go toward infinity in the root locus plot.
![[Pasted image 20240301093207.png]]
This is used for calculating the centroid of the asymptote.

### Summary
![[Pasted image 20240301093615.png]]
![[Pasted image 20240301093627.png]]
![[Pasted image 20240301093640.png]]
