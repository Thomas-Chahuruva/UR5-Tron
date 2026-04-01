\# UR5-Tron: 6-DOF Robotic Digital Twin



\*\*Engineer:\*\* Thomas Chahuruva  

\*\*Project Initiation:\*\* March 2026  

\*\*Status:\*\* V2 Architecture Complete (Designing Phase)



\## 📌 Executive Summary

This repository contains the complete mechanical engineering and design record for \*\*TRON\*\*, a six-degree-of-freedom (6-DOF) serial robotic arm. The project bridges physical CAD geometry with software-in-the-loop control logic, resulting in a redundancy-free digital twin capable of validating spatial trajectories and inverse kinematics within a MATLAB/Simscape physics engine.


The core objective was to engineer a high-stiffness, mass-optimized desktop manipulator capable of handling a \*\*500g payload\*\*, utilizing commercially available NEMA 17 actuators and planetary reductions. Every design decision is evaluated against a strict \*\*Safety Factor of 1.5\*\*.



\## ⚙️ System Architecture \& Actuator Specifications

The kinematic chain was aggressively optimized to strip distal mass, reducing the moment arm load on the critical shoulder and base joints.



| Joint | Function | Drive System 



| \*\*J1\*\* | Base Yaw | NEMA 17 + 27:1 Planetary 

| \*\*J2\*\* | Shoulder Pitch | NEMA 17 + 27:1 Planetary 

| \*\*J3\*\* | Elbow Pitch | NEMA 17 + 19:1 Planetary

| \*\*J4\*\* | Wrist Pitch | NEMA 17 + 3:1 Reducer 

| \*\*J5\*\* | Wrist Yaw | NEMA 17 Pancake (Direct) 

| \*\*J6\*\* | End Effector | NEMA 17 Pancake (Direct)









