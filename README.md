\# UR5-Tron: 6-DOF Robotic Digital Twin



\*\*Engineer:\*\* Thomas Chahuruva  

\*\*Project Initiation:\*\* March 2026  

\*\*Status:\*\* V2 Architecture Complete (Designing Phase)



\## 📌 Executive Summary

This repository contains the complete mechanical engineering and design record for \*\*TRON\*\*, a six-degree-of-freedom (6-DOF) serial robotic arm. The project bridges physical CAD geometry with software-in-the-loop control logic, resulting in a redundancy-free digital twin capable of validating spatial trajectories and inverse kinematics within a MATLAB/Simscape physics engine.



The core objective was to engineer a high-stiffness, mass-optimized desktop manipulator capable of handling a \*\*500g payload\*\* at a \*\*512mm reach\*\*, utilizing commercially available NEMA 17 actuators and planetary reductions. Every design decision is evaluated against a strict \*\*Safety Factor of 1.5\*\*.



\## ⚙️ System Architecture \& Actuator Specifications

The kinematic chain was aggressively optimized to strip distal mass, reducing the moment arm load on the critical shoulder and base joints.



| Joint | Function | Drive System | Static Torque Output | Margin (vs. Peak Load) |



| \*\*J1\*\* | Base Yaw | NEMA 17 + 27:1 Planetary | 9.18 Nm | +32% |

| \*\*J2\*\* | Shoulder Pitch | NEMA 17 + 27:1 Planetary | 9.18 Nm | +82.5% |

| \*\*J3\*\* | Elbow Pitch | NEMA 17 + 19:1 Planetary | 6.46 Nm | +172% |

| \*\*J4\*\* | Wrist Pitch | NEMA 17 + 3:1 Reducer | 1.02 Nm | +63% |

| \*\*J5\*\* | Wrist Yaw | NEMA 17 Pancake (Direct) | 0.10 Nm | +669% |

| \*\*J6\*\* | End Effector | NEMA 17 Pancake (Direct) | 0.10 Nm | +33% |



\## 🧠 Engineering The Bottleneck: Kinematic Locking

A critical challenge in multibody dynamic simulation is overcoming "Kinematic Locking" a scenario where standard structural CAD mates over-constrain the degrees of freedom, causing matrix singularities and crashing the physics engine. 



To solve this, the spatial constraint logic was completely overhauled. A strict, redundancy-free \*\*"Concentric + Coincident"\*\* mating strategy was deployed across all joint clusters (J1-J6). This solution successfully enabled the engine to calculate mass inertia, gravitational loads, and dynamic motion accurately, establishing a robust pipeline for advanced control systems testing.









