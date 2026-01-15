# Step-by-Step Guide: Finding Lagrangian Dynamics from Forward Kinematics

Lagrangian dynamics is a powerful approach to deriving the equations of motion for robotic systems. This method involves using the difference between kinetic and potential energies to obtain the dynamics of the system. In this guide, we will walk through the steps to derive the Lagrangian dynamics, assuming that the forward kinematics are known.

## Prerequisites
- **Forward Kinematics**: The position and velocity of the robot’s end-effector as functions of the joint variables.
- **Kinematics of Joints**: Expressions for position, velocity, and acceleration of each link.
- Basic knowledge of calculus and physics, specifically classical mechanics.

## Steps

### 1. Define the Generalized Coordinates
The generalized coordinates are the joint variables that describe the configuration of the robot. For an $n$-degree-of-freedom (DOF) robot:
- $\mathbf{q} = [q_1, q_2, \dots, q_n]$ where $q_i$ represents the joint angle (for revolute joints) or displacement (for prismatic joints).

The generalized coordinates can be either angles for revolute joints or linear displacements for prismatic joints.

### 2. Write the Forward Kinematics
Using forward kinematics, express the position of each link in terms of the generalized coordinates $\mathbf{q}$.

For each link $i$, you should know the position $\mathbf{p}_i$ and the orientation $R_i$ as functions of $\mathbf{q}$:

$$
\mathbf{p}_i = f_i(\mathbf{q})
$$

Where $\mathbf{p}_i$ represents the position of the center of mass of link $i$.

### 3. Compute the Velocity of Each Link
To find the kinetic energy, you need the velocity of each link. Use the chain rule to find the velocity $\dot{\mathbf{p}}_i$ of the center of mass of each link:

$$
\dot{\mathbf{p}}_i = \frac{d}{dt} f_i(\mathbf{q})
$$

This can be expressed as:

$$
\dot{\mathbf{p}}_i = J_i(\mathbf{q}) \dot{\mathbf{q}}
$$

Where $J_i(\mathbf{q})$ is the Jacobian matrix of link $i$, which relates joint velocities $\dot{\mathbf{q}}$ to the velocity of the link’s center of mass.

### 4. Compute the Kinetic Energy
The kinetic energy $T$ of the robot is the sum of the kinetic energies of all the links. For each link $i$, the kinetic energy is given by:

$$
T_i = \frac{1}{2} m_i \|\dot{\mathbf{p}}_i\|^2 + \frac{1}{2} \dot{\mathbf{q}}^T I_i \dot{\mathbf{q}}
$$

Where:
- $m_i$ is the mass of link $i$.
- $\|\dot{\mathbf{p}}_i\|^2$ is the squared velocity magnitude of the link’s center of mass.
- $I_i$ is the inertia matrix of link $i$ around its center of mass.
- $\dot{\mathbf{q}}^T I_i \dot{\mathbf{q}}$ represents the rotational kinetic energy of link $i$.

The total kinetic energy $T$ of the system is the sum over all links:

$$
T = \sum_{i=1}^n T_i
$$

### 5. Compute the Potential Energy
The potential energy $V$ of the robot comes from gravitational forces acting on each link. For each link $i$, the potential energy is:

$$
V_i = m_i g \mathbf{z}^T \mathbf{p}_i
$$

Where:
- $m_i$ is the mass of link $i$.
- $g$ is the acceleration due to gravity.
- $\mathbf{z}$ is the unit vector in the direction of gravity (usually along the negative $z$-axis in Cartesian coordinates).
- $\mathbf{p}_i$ is the position of the center of mass of link $i$.

The total potential energy $V$ is the sum over all links:

$$
V = \sum_{i=1}^n V_i
$$

### 6. Form the Lagrangian
The Lagrangian $\mathcal{L}$ is defined as the difference between the total kinetic energy and the total potential energy:

$$
\mathcal{L} = T - V
$$

### 7. Apply the Euler-Lagrange Equation
To derive the equations of motion, apply the **Euler-Lagrange equation** to each generalized coordinate $q_i$:

$$
\frac{d}{dt} \left( \frac{\partial \mathcal{L}}{\partial \dot{q}_i} \right) - \frac{\partial \mathcal{L}}{\partial q_i} = \tau_i
$$

Where:
- $\tau_i$ is the generalized force or torque acting on joint $i$.
- $\frac{\partial \mathcal{L}}{\partial \dot{q}_i}$ represents the partial derivative of the Lagrangian with respect to the velocity of $q_i$.
- $\frac{\partial \mathcal{L}}{\partial q_i}$ represents the partial derivative of the Lagrangian with respect to the position of $q_i$.

### 8. Solve for the Equations of Motion
After applying the Euler-Lagrange equation, you will obtain a set of second-order differential equations that describe the motion of the system. These equations can be expressed in the following form:

$$
M(\mathbf{q}) \ddot{\mathbf{q}} + C(\mathbf{q}, \dot{\mathbf{q}}) \dot{\mathbf{q}} + G(\mathbf{q}) = \boldsymbol{\tau}
$$

Where:
- $M(\mathbf{q})$ is the **mass (inertia) matrix**.
- $C(\mathbf{q}, \dot{\mathbf{q}})$ represents the **Coriolis and centrifugal forces**.
- $G(\mathbf{q})$ is the **gravity vector**.
- $\boldsymbol{\tau}$ is the vector of joint torques.

### 9. Validate the Dynamics Model
Once you have the equations of motion, you should validate them by:
- Simulating the dynamics using software (MATLAB, Python, etc.).
- Comparing the results with known analytical solutions for simpler systems or experimental data for real robots.

## Example: 2-Link Planar Robot
Consider a simple 2-link planar robot with revolute joints. The position of the end-effector can be expressed as:

$$
x = l_1 \cos(q_1) + l_2 \cos(q_1 + q_2)
$$
$$
y = l_1 \sin(q_1) + l_2 \sin(q_1 + q_2)
$$

1. **Velocity**:
   Use the Jacobian to find the velocity of the end-effector:
   $$
   \dot{\mathbf{p}} = J(\mathbf{q}) \dot{\mathbf{q}}
   $$

2. **Kinetic energy**:
   The total kinetic energy is:
   $$
   T = \frac{1}{2} m_1 \|\dot{\mathbf{p}}_1\|^2 + \frac{1}{2} m_2 \|\dot{\mathbf{p}}_2\|^2
   $$

3. **Potential energy**:
   The potential energy is:
   $$
   V = m_1 g y_1 + m_2 g y_2
   $$

4. **Lagrangian**:
   $$
   \mathcal{L} = T - V
   $$

Apply the Euler-Lagrange equation to derive the equations of motion.

## Conclusion
The Lagrangian method provides a systematic approach to deriving the dynamic equations of a robot. By using the forward kinematics to compute the kinetic and potential energy, and applying the Euler-Lagrange equations, you can derive the full dynamic model of the robot.

## References
- [Lagrangian Mechanics](https://en.wikipedia.org/wiki/Lagrangian_mechanics)
- [Introduction to Robotics: Mechanics and Control by John J. Craig]
