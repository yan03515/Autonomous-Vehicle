# Autonomous-Vehicle
## Summary
This repository introduces the autonomous vehicle platform used in my master’s project at NTUST. I participated in the vehicle’s assembly, system integration, modification, debugging, and testing, including its mechanical structure, FPGA-based motor control, and PC-side control program.The vehicle serves as the physical platform for my research on autonomous vehicle localization and future navigation development. Therefore, understanding and integrating the complete control system—from high-level motion commands to low-level motor actuation—is an important part of the project.  
The purpose of this README is not to provide detailed source-code documentation, but to give an overview of how the vehicle operates, the modifications and engineering work I performed, the testing results, and the planned improvements for autonomous navigation.

## System Workflow

<p align="center">
  <img src="images/Autonomous%20Vehicle%20Control%20System%20Workflow.png" width="900">
</p>

The workflow consists of three main stages: building the PC-side control program, configuring the FPGA, and running the vehicle control system. The control program is compiled in Visual Studio and deployed to the DE2i-150 host PC, while the FPGA project is compiled in Quartus Prime 16.1 Lite Edition and configured through USB-Blaster. During operation, keyboard commands are processed by the PC-side control program, sent to the FPGA through PCIe, converted into PWM/GPIO control signals, and then passed to the ESCON motor drivers to drive the four motors.

## My Contributions

### Vehicle Structure

I modified the vehicle platform by replacing the original wheels with **8-inch Mecanum wheels**. The larger wheels improve the vehicle’s ability to pass over uneven pavement and small road irregularities, providing a more stable platform for future onboard sensors and autonomous navigation experiments.

### PC-side Control Program

I developed the current **PC-side control program in C++ using Visual Studio** for manual vehicle control and hardware testing. The program converts keyboard inputs into vehicle motion commands, calculates the corresponding commands for the four Mecanum wheels using vehicle kinematics, and sends the motor-control values to the FPGA through PCIe.

The program also reads encoder data from the FPGA for wheel-speed monitoring and system validation. The current control loop operates at **200 Hz**, allowing control commands and feedback data to be updated continuously during operation.

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

![Vehicle Testing](images/vehicle_test.gif)
