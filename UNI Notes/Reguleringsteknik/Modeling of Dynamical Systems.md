## Models
Models are given by diffferential equations or algebraic relations

### Example (Mass Spring Damper)
- The force F is considered to be the input
- The mass velocity is considered to be the output of the system
The system is of second order, since the dynamics of the system depends on both
position and velocity
![[Pasted image 20240202083127.png]]
The system model is given by Newton’s second law
$$mp''=-kp-bp'+F$$
where F is the input (corresponds to u in the drawing)
The output y of the system is given by the relation
$$y=p'$$
It is seen that the system model comprises
- a 2nd order differential equation (given by Newton’s second law) and
- an algebraic relation (output relation)

# Linear Time-Invariant Systems
![[Pasted image 20240202083445.png]]
![[Pasted image 20240202083526.png]]
## Time invariant
The response of the system does not change due to time passing.

## Mass Spring Damper example
![[Pasted image 20240202083729.png]]
## Relation between Models
![[Pasted image 20240202101138.png]]
# Time Domain models
![[Pasted image 20240202091856.png]]
## Continuous-Time State Space Models
![[Pasted image 20240202091944.png]]

### Transformation to State Space form
![[Pasted image 20240202092133.png]]
To transform a differential equation into state space form, the following procedure can be
followed, when z is the unknown function.
1. Define variables $x_i$ according to $x_1$ = z, $x_2$ = $z'$, . . . , $x_n = z^{(n−1)}$.
2. Define the system matrix $A ∈ R^{n×n}$ and input matrix $B ∈ R^{n×m}$ as
![[Pasted image 20240202092353.png]]

#### Mass Spring Damper Example
Recall the dynamics of the mass-spring-damper system
$$m\ddot{p}=-kp-b\dot{p}+F$$
where p is the position of the mass and F is the input force.
![[Pasted image 20240202093328.png]]

### Solution to differential equation
![[Pasted image 20240202094121.png]]
![[Pasted image 20240202094145.png]]

## Discrete-Time State Space Models
![[Pasted image 20240202094601.png]]

## Transformation from continous time to discrete time
![[Pasted image 20240202094740.png]]
System is time-invariant, so the specific time does not matter, only the time-step T.
![[Pasted image 20240202095040.png]]

### Mass Spring Damper system
![[Pasted image 20240202095237.png]]

# Frequency Domain Models
## State Space Model to Transfer Function
![[Pasted image 20240202095556.png]]
![[Pasted image 20240202095756.png]]
![[Pasted image 20240202095931.png]]

### Mass Spring Damper Example
![[Pasted image 20240202100000.png]]
![[Pasted image 20240202100049.png]]

## Transfer function to State Space Model
![[Pasted image 20240202100738.png]]
![[Pasted image 20240202100756.png]]
## Discrete Transfer functions
![[Pasted image 20240202100821.png]]
![[Pasted image 20240202100834.png]]
![[Pasted image 20240202100849.png]]
### Discretization Methods
![[Pasted image 20240202101024.png]]