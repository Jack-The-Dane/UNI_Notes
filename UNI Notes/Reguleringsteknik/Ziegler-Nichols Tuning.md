Sometimes a model of the plant is not available, then the controller should be tuned by
only studying the input-output behavior of the system.
Zeigler and Nichols has proposed two methods for tuning PID controllers without explicit use of a plant model
-  Zeigler-Nichols tuning based on step response
-  Zeigler-Nichols tuning - The ultimate sensitivity method
**By using the Ziegler-Nichols tuning method, a closed-loop system is obtained that has a
decay ratio of ∼ 0.25 (damping ration ζ ≈ 0.21).**
# Based on step response
## Finding transfer function of system
![[Pasted image 20240223092428.png]]
## Finding gains of controller
![[Pasted image 20240223092638.png]]

# Ultimate sensitivity method
![[Pasted image 20240223093049.png]]
**The period of the oscillation $P_u$ is called the ultimate period.**
## Finding gains
![[Pasted image 20240223093201.png]]

## Example
![[Pasted image 20240223093307.png]]
![[Pasted image 20240223093323.png]]
