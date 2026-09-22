# Autonomous-Vehicle
## Summary
This repository introduces the autonomous vehicle platform used in my master’s project at NTUST. I participated in the vehicle’s assembly, system integration, modification, debugging, and testing, including its mechanical structure, FPGA-based motor control, and PC-side control program.The vehicle serves as the physical platform for my research on autonomous vehicle localization and future navigation development. Therefore, understanding and integrating the complete control system—from high-level motion commands to low-level motor actuation—is an important part of the project.  
The purpose of this README is not to provide detailed source-code documentation, but to give an overview of how the vehicle operates, the modifications and engineering work I performed, the testing results, and the planned improvements for autonomous navigation.

## System Workflow

<p align="center">
  <img src="images/Autonomous%20Vehicle%20Control%20System%20Workflow.png" width="900">
</p>

The workflow consists of three main stages: building the PC-side control program, configuring the FPGA, and running the vehicle control system. The control program is compiled in Visual Studio and deployed to the DE2i-150 host PC, while the FPGA project is compiled in Quartus Prime 16.1 Lite Edition and configured through USB-Blaster. During operation, keyboard commands are processed by the PC-side control program, sent to the FPGA through PCIe, converted into PWM/GPIO control signals, and then passed to the ESCON motor drivers to drive the four motors.
