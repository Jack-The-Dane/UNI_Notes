## Problem Formulation
![[Pasted image 20240426083158.png]]
positive semi-definite: Eigen-values are equal to or bigger than zero
Positive definite: Eigen-values are bigger than zero.
R is the "price" associated with using your input signal, which is why if R is zero, the best solution will always be to increase your input signal.
If Q is zero, it means that there are no requirements for the solution, and therefore the best solution will be to set u to zero, as the cost function will always be zero then.

if Q is set to:
$$Q = C^T 
\begin{bmatrix}
a & 0 \\
0 & b
\end{bmatrix} C$$
Then $x^TQx$ becomes:
$$x^TQx = 
\begin{bmatrix}
y_1 & y_2
\end{bmatrix} 
\begin{bmatrix}
a & 0 \\
0 & b
\end{bmatrix}
\begin{bmatrix}
y_1 \\
y_2
\end{bmatrix}$$
This way you can optimise for one of the output signals over the other in the cost function.

## The algebraic Riccati Equation
![[Pasted image 20240426085406.png]]

## Optimal state feedback control
![[Pasted image 20240426085431.png]]

## Output variance minimization
![[Pasted image 20240426085516.png]]

## Tuning using Bryson's rule
![[Pasted image 20240426085548.png]]

## Optimal State Estimation
![[Pasted image 20240426085702.png]]
![[Pasted image 20240426085712.png]]
