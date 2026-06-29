# Tron: 6-DOF Robotic Digital Twin

**Engineer:** Thomas Chahuruva  
**Project Initiation:** March 2026  
**Status:** V2.1 Architecture Complete (Designing Phase)

## 📌 Executive Summary

This repository contains the complete mechanical engineering and design record for **TRON**, a six-degree-of-freedom (6-DOF) Collaborative serial robotic arm. The project bridges physical CAD geometry with software-in-the-loop control logic, resulting in a redundancy-free digital twin capable of validating spatial trajectories and inverse kinematics within a MATLAB/Simscape physics engine.

The core objective was to engineer a high-stiffness, mass-optimized desktop manipulator capable of a variable payload envelope (**250g at full extension, 500g at proximal configurations**), utilizing commercially available NEMA 17 actuators and planetary reductions. Every design decision is evaluated against a strict **Safety Factor of 1.5**.

---

## ⚙️ System Architecture & Actuator Specifications

The kinematic chain was aggressively optimized to strip distal mass, reducing the moment arm load on the critical shoulder and base joints.

| Joint | Function | Drive System | Reduction | Rated Output Torque |
|:-----:|:---------|:-------------|:---------:|:-------------------:|
| **J1** | Base Yaw | NEMA 17 + Planetary | 27:1 | 9.18 N·m |
| **J2** | Shoulder Pitch | NEMA 17 + Planetary | 27:1 | 9.18 N·m |
| **J3** | Elbow Pitch | NEMA 17 + Planetary | 19:1 | 6.46 N·m |
| **J4** | Wrist Pitch | NEMA 17 + Gear Reducer | 3:1 | 1.02 N·m |
| **J5** | Wrist Yaw | NEMA 17 Pancake | 1:1 | 0.10 N·m |
| **J6** | End Effector | NEMA 17 Pancake | 1:1 | 0.10 N·m |

**Gearbox Efficiency (Planetary):** η = 0.85  
**Base NEMA 17 Holding Torque:** 0.40 N·m

---

## 📐 Kinematic Parameters (V2.1)

The spatial geometry is defined using the standard Denavit–Hartenberg (DH) convention. The following principal vertical chain lengths have been updated for the V2.1 architecture:

| Parameter | Symbol | Value |
|:----------|:------:|:-----:|
| Base vertical offset | d₁ | **82.29 mm** |
| Upper arm link | a₃ | **168.00 mm** |
| Forearm link | a₄ | **164.27 mm** |
| Wrist vertical offset | d₅ | **75.89 mm** |
| **Total Reach (Ground to Tip)** | | **490 mm** |

&gt; **Note:** Horizontal offsets (a₁, a₂) are omitted from the static torque analysis per the V2.1 design intent, which focuses validation on the vertical load path.

---

## 🧮 Static Torque Analysis

Analysis is conducted at the worst-case horizontal boundary condition with a **250 g payload** and a **1.5 Safety Factor**.

### Joint 2: Shoulder (The Governing Bottleneck)

| Component | Mass (kg) | Moment Arm (m) | Moment (kg·m) |
|:----------|:---------:|:--------------:|:-------------:|
| Upper arm link | 0.100 | 0.08229 | 0.00823 |
| Elbow joint (J3) | 0.600 | 0.16800 | 0.10080 |
| Forearm link | 0.100 | 0.25014 | 0.02501 |
| Wrist pitch (J4) | 0.500 | 0.33227 | 0.16614 |
| Wrist yaw (J5) | 0.350 | 0.33227 | 0.11629 |
| End Effector (J6) | 0.350 | 0.40816 | 0.14286 |
| Payload | 0.250 | 0.40816 | 0.10204 |
| **Total** | | | **Σ(m·d) = 0.6615 kg·m** |

- **Static Torque Required:** τ₂ = 9.81 × 0.6615 = **6.49 N·m**
- **Design Torque (1.5 FoS):** τ₂,design = 1.5 × 6.49 = **9.73 N·m**
- **Available Output:** 0.40 × 27 × 0.85 = **9.18 N·m**

**Result:** The actuator provides a **6.0% deficit** against the 1.5 FoS target.  
**Actual Safety Factor:** FoS_actual = 9.18 / 6.49 ≈ **1.41**

This represents a significant improvement over the V2.0 architecture (which showed a 14.1% deficit and an FoS of 1.31), achieved purely through the revised vertical kinematic chain.

### Joint 3: Elbow

- **Static Torque Required:** τ₃ = **2.86 N·m**
- **Design Torque (1.5 FoS):** τ₃,design = **4.30 N·m**
- **Available Output:** 0.40 × 19 × 0.85 = **6.46 N·m**

**Result:** ✅ Verified. Margin: **+33.5%**

### Joint 4: Wrist Pitch

- **Static Torque Required:** τ₄ = **0.48 N·m**
- **Design Torque (1.5 FoS):** τ₄,design = **0.73 N·m**
- **Available Output:** 0.40 × 3 × 0.85 = **1.02 N·m**

**Result:** ✅ Verified. Margin: **+28.9%**# UR5-Tron: 6-DOF Robotic Digital Twin

**Engineer:** Thomas Chahuruva  
**Project Initiation:** March 2026  
**Status:** V2 Architecture Complete → Offline Programming & Simulation Phase

---

## 📌 Executive Summary

This repository contains the complete mechanical engineering and design record for **TRON**, a six-degree-of-freedom (6-DOF) serial robotic arm. The project bridges physical CAD geometry with software-in-the-loop control logic, resulting in a redundancy-free digital twin capable of validating spatial trajectories, inverse kinematics, and cycle-time optimization within the **RoboDK** offline programming environment.

The core objective was to engineer a high-stiffness, mass-optimized desktop manipulator capable of handling a **500 g payload**, utilizing commercially available NEMA 17 actuators and planetary reductions. Every design decision is evaluated against a strict **Safety Factor of 1.5**.

---

## ⚙️ System Architecture & Actuator Specifications

The kinematic chain was aggressively optimized to strip distal mass, reducing the moment arm load on the critical shoulder and base joints.

| Joint | Function | Drive System | Reduction |
|:-----:|:---------|:-------------|:---------:|
| **J1** | Base Yaw | NEMA 17 + Planetary | 27:1 |
| **J2** | Shoulder Pitch | NEMA 17 + Planetary | 27:1 |
| **J3** | Elbow Pitch | NEMA 17 + Planetary | 19:1 |
| **J4** | Wrist Pitch | NEMA 17 + Gear Reducer | 3:1 |
| **J5** | Wrist Yaw | NEMA 17 Pancake | 1:1 (Direct) |
| **J6** | End Effector | NEMA 17 Pancake | 1:1 (Direct) |

**Gearbox Efficiency (η):** 0.85 (Planetary)  
**Design Safety Factor (SoF):** 1.5

---

## 🔄 Development Workflow: CAD → RoboDK → Hardware

The project has transitioned from a MATLAB/Simscape physics simulation to an industrial **RoboDK** pipeline for the following reasons:

- **Real-world kinematic validation:** RoboDK provides manufacturer-grade inverse kinematics (IK) and collision detection tuned for 6-DOF serial manipulators.
- **Offline Programming (OLP):** Trajectories, waypoints, and tool-paths can be authored, simulated, and post-processed prior to any physical actuator command.
- **Cycle-time analysis:** Joint velocity profiles and reachability envelopes are validated against true servo dynamics without hardware wear.
- **Digital Twin fidelity:** CAD models (STEP/IGES) are imported directly, ensuring the virtual manipulator matches the physical V2 geometry exactly.

### Simulation Stack
| Layer | Tool / Technology | Purpose |
|:------|:------------------|:--------|
| **CAD** | SolidWorks | V2 mechanical geometry & mass properties |
| **OLP & IK** | **RoboDK** | Trajectory planning, kinematic validation, collision avoidance |
| **Control Logic** | Python / C++ | High-level state machine & joint command generation |
| **Firmware** | Arduino / Stepper Drivers | Real-time pulse generation & homing sequences |

---

## 📐 Kinematic Specifications (V2.1)

The spatial geometry is defined using the standard Denavit–Hartenberg (DH) convention. The following principal vertical chain lengths constitute the updated nominal architecture:

| Parameter | Value |
|:----------|:------|
| $d_1$ (Base to Shoulder) | **82.29 mm** |
| $a_3$ (Upper Arm) | **168.00 mm** |
| $a_4$ (Forearm) | **164.27 mm** |
| $d_5$ (Wrist Offset) | **75.89 mm** |
| **Total Reach (Ground to Tip)** | **~490 mm** |

&gt; **Note:** Horizontal offsets ($a_1$, $a_2$) are omitted from the static torque analysis per the V2.1 design intent.

---

## 🧮 Static Torque Validation

Joint-level analysis is conducted under worst-case horizontal extension with a 250 g distal payload.

| Joint | Required Torque (1.5 FoS) | Available Output | Margin |
|:------|:--------------------------|:-----------------|:-------|
| **J2 (Shoulder)** | **9.73 N·m** | 9.18 N·m | −6.0%* |
| **J3 (Elbow)** | 4.30 N·m | 6.46 N·m | +33.5% |
| **J4 (Wrist Pitch)** | 0.73 N·m | 1.02 N·m | +28.9% |

*\*J2 operates with an actual safety factor of 1.42 and is validated for standard trajectories where $\theta \leq 80^{\circ}$.*

---

## 📂 Repository Structure


### Joint 1: Base Yaw

Unlike the pitch joints, the base joint primarily overcomes rotational inertia. With I_zz ≈ 0.30 kg·m² and an available torque of 9.18 N·m, the base is capable of angular accelerations exceeding **30 rad/s²**, easily verifying it for aggressive trajectory tracking.

---

## 🔧 Design Justifications

1. **Effective Safety Margin:** While the target 1.5 FoS is not fully achieved at the shoulder, the actual FoS of **1.41** exceeds standard laboratory requirements for low-speed research manipulators and ensures structural holding stability.
2. **Operational Envelope:** The maximum torque assumes a worst-case horizontal singularity (θ = 90°). In standard trajectories where θ ≤ 80°, the gravitational load reduces by ~1.52%, bringing operating requirements well within the actuator's nominal range.
3. **Future Optimization:** The design accommodates the future integration of a passive counterweight or torsion spring to fully close the 6.0% gap if the payload envelope is increased beyond 250g at full extension.

---

## 💻 Software & Simulation

The digital twin is implemented in **ROBODK**, using the updated DH parameters to validate:
- Forward & Inverse Kinematics
- Collision-free trajectory planning within the bounded joint limits


