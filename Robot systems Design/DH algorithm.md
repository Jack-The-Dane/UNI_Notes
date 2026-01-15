# Step-by-Step Guide: Assigning Frames to Robots Using the DH Algorithm

The Denavit-Hartenberg (DH) algorithm is used to systematically assign reference frames to the joints and links of a robot manipulator. This guide will walk you through the steps to assign frames based on the DH convention.

## Prerequisites
- Basic understanding of kinematics and robotic manipulator structure.
- Familiarity with matrix transformations (rotation and translation matrices).

## Steps

### 1. Understand the Robot Structure
- **Identify each joint and link** in the robot manipulator.
  - **Revolute joints**: Joints that rotate about an axis.
  - **Prismatic joints**: Joints that translate along an axis.
- Each joint connects one link to the next in a chain.

### 2. Define the Link and Joint Variables
For each link in the robot, we define four parameters:
- $\theta$ (theta): Joint angle (for revolute joints).
- $d$: Link offset (distance along the Z-axis).
- $a$: Link length (distance along the X-axis).
- $\alpha$ (alpha): Twist angle (rotation around the X-axis).

### 3. Assign Coordinate Frames to Each Joint
For each joint (starting from the base):
1. **Z-axis**: Align the Z-axis with the axis of motion (rotation or translation) of the joint.
   - Revolute joint: Z-axis is along the axis of rotation.
   - Prismatic joint: Z-axis is along the direction of translation.
2. **X-axis**: Define the X-axis perpendicular to both the current Z-axis and the next Z-axis.
   - This is along the common normal between successive Z-axes.

Repeat these steps for each joint.

### 4. Determine the DH Parameters
For each pair of consecutive links, calculate the following DH parameters:
- $\theta$: The angle between the X-axes of the current and the next frame, measured in the plane normal to the Z-axis.
  - For revolute joints, $\theta$ is variable and changes as the joint rotates.
- $d$: The distance along the Z-axis between the origins of the two frames.
  - For prismatic joints, $d$ is variable and changes as the joint translates.
- $a$: The distance between the Z-axes of two consecutive frames, measured along the X-axis.
- $\alpha$: The angle between the Z-axes of the two consecutive frames, measured about the X-axis.

### 5. Create the DH Transformation Matrix
For each joint, use the following standard DH transformation matrix:

$$
T_{i-1}^{i} =
\begin{bmatrix}
\cos \theta_i & -\sin \theta_i \cos \alpha_i & \sin \theta_i \sin \alpha_i & a_i \cos \theta_i \\
\sin \theta_i & \cos \theta_i \cos \alpha_i & -\cos \theta_i \sin \alpha_i & a_i \sin \theta_i \\
0 & \sin \alpha_i & \cos \alpha_i & d_i \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

Where:
- $\theta_i$: Joint angle.
- $d_i$: Link offset.
- $a_i$: Link length.
- $\alpha_i$: Twist angle.

### 6. Multiply the Transformation Matrices
- For each link, multiply the transformation matrices sequentially:
  
$$
T_0^n = T_0^1 \cdot T_1^2 \cdot T_2^3 \cdots T_{n-1}^n
$$

This matrix describes the position and orientation of the end effector relative to the base frame.

### 7. Verify Frame Assignments
- **Check the frames**: Ensure that all coordinate frames follow the DH convention.
- **Consistency**: Each frame should be consistent with the robot's physical structure and constraints.

## Example: 2-Link Robot Arm
Consider a simple 2-link planar robot with two revolute joints.
1. **Joint 1**: Assign frame 1 at the base, $Z_1$ along the axis of rotation, and $X_1$ along the first link.
2. **Joint 2**: Assign frame 2 at the end of the first link, with $Z_2$ along the axis of rotation and $X_2$ along the second link.
3. Calculate DH parameters ($\theta_1, d_1, a_1, \alpha_1$ for link 1, and $\theta_2, d_2, a_2, \alpha_2$ for link 2).

## Conclusion
Using the DH algorithm allows you to systematically define the reference frames for any robotic manipulator. With these frames, you can easily calculate forward kinematics and determine the end-effector’s position and orientation relative to the base.

## References
- [Robot Kinematics: Denavit-Hartenberg Parameters](https://en.wikipedia.org/wiki/Denavit%E2%80%93Hartenberg_parameters)
- [Introduction to Robotics: Mechanics and Control by John J. Craig]
