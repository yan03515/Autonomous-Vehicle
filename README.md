# Autonomous-Vehicle
## Summary
This repository introduces the autonomous vehicle platform used in my master’s project at NTUST. I participated in the vehicle’s assembly, system integration, modification, debugging, and testing, including its mechanical structure, FPGA-based motor control, and PC-side control program. The vehicle serves as the physical platform for my research on autonomous vehicle localization and future navigation development. Therefore, understanding and integrating the complete control system—from high-level motion commands to low-level motor actuation—is an important part of the project.  
The purpose of this README is not to provide detailed source-code documentation, but to give an overview of how the vehicle operates, the modifications and engineering work I performed, the vehicle testing demonstrations, and the planned improvements for autonomous navigation.

## System Workflow

<p align="center">
  <img src="images/Autonomous%20Vehicle%20Control%20System%20Workflow.png" width="900">
</p>

The workflow consists of three main stages: building the PC-side control program, configuring the FPGA, and running the vehicle control system. The control program is compiled in Visual Studio and deployed to the DE2i-150 host PC, while the FPGA project is compiled in Quartus Prime 16.1 Lite Edition and configured through USB-Blaster. During operation, keyboard commands are processed by the PC-side control program, sent to the FPGA through PCIe, converted into PWM/GPIO control signals, and then passed to the ESCON motor drivers to drive the four motors.

## My Contributions

### Vehicle Structure

I modified the vehicle platform by replacing the original wheels with **8-inch Mecanum wheels**. The larger wheels are intended to improve the vehicle’s ability to pass over uneven pavement and small road irregularities, providing a more stable platform for future onboard sensors and autonomous navigation experiments.

### PC-side Control Program

I developed the current **PC-side control program in C++ using Visual Studio** for manual vehicle control and hardware testing. The program converts keyboard inputs into vehicle motion commands, calculates the corresponding commands for the four Mecanum wheels using vehicle kinematics, and sends the motor-control values to the FPGA through PCIe.

The program also reads encoder data from the FPGA for wheel-speed monitoring and system validation. The control loop is configured to operate at **200 Hz**, allowing control commands and feedback data to be updated continuously during operation.

### FPGA Program

Based on knowledge gained from related coursework, I reviewed the FPGA source code and hardware signal flow to understand the PCIe register mapping, PWM generation, and FPGA I/O configuration.

During vehicle testing, one wheel initially failed to operate correctly. I systematically checked the control logic, FPGA signal path, and hardware connections, and eventually identified the issue as an FPGA pin-assignment problem. I then reassigned the corresponding FPGA output pins, recompiled the design in **Quartus Prime 16.1 Lite Edition**, programmed the FPGA, and successfully restored normal motor operation.

## Vehicle Structure and Testing

### Structure
- Whole Vehicle

<p align="center">
  <img src="images/Whole%20Vehicle.png" width="500">
</p>

- Control Hardware

<p align="center">
  <img src="images/Control%20Hardware.png" width="500">
</p>

- 8-inch Mecanum Wheel

<p align="center">
  <img src="images/Mecanum%20Wheel.png" width="500">
</p>

### Testing

<p align="center">
  <img src="images/Vehicle%20Test.gif" width="500">
</p>

## Future Development for Autonomous Navigation

Future development will focus on three main areas to support autonomous navigation and improve the vehicle's overall performance.

### 1. Mechanical Improvements

Road-induced vibrations during vehicle operation may affect the measurement quality of onboard sensors, particularly LiDAR and IMU.

To address this issue, future modifications will include developing a **suspension and vibration isolation system**, referencing mechanical designs available on GrabCAD. Additionally, the **LiDAR mounting position will be raised** to reduce potential sensor occlusion and improve environmental coverage while maintaining structural stability.

### 2. Autonomous Navigation Integration

This vehicle will serve as the **real-world testing platform for my [Master-Project](https://github.com/yan03515/Master-Project)**, supporting the development and validation of autonomous navigation on the NTUST campus.

The existing **PC-side control program** will be extended to receive navigation commands through **ROS**, replacing keyboard-only control and enabling autonomous operation. This will involve integrating navigation commands with the vehicle's motor control system and encoder feedback.

### 3. Control System Optimization

The system's real-time performance will be evaluated during autonomous navigation, including control latency, command response, and communication between the PC and FPGA.

If performance bottlenecks are identified, the **PC-side control program** will be optimized, with modifications to the **low-level FPGA logic** considered where necessary.

Additional safety mechanisms, such as emergency stopping, command timeouts, and velocity limits, may also be implemented as needed.
