# Model Predictive Control - Porsche Taycan - Slope

[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=simorxb/taycan-MPC-slope)

## Summary
This project demonstrates the application of Model Predictive Control (MPC) to regulate the speed of a Porsche Taycan model under the influence of road slope disturbances. The primary goal is to test the robustness of the MPC algorithm when subjected to constant disturbances, such as varying road slopes, and evaluate its performance in achieving smooth control with minimal overshoot.

## Project Overview

### Plant Model - Porsche Taycan
The dynamic model represents a car of mass $m$, propelled by a force $F$, and influenced by aerodynamic drag $-0.5 \cdot C_d \cdot A \cdot \rho \cdot v^2$, where:
- $C_d$: Drag coefficient
- $A$: Reference area
- $\rho$: Air density
- $v$: Speed

Additionally, the model incorporates the road slope $\theta$ and is governed by the equation:

$$m \cdot \frac{dv}{dt} = F - 0.5 \cdot C_d \cdot A \cdot \rho \cdot v^2 - m \cdot g \cdot \sin(\theta)$$

#### Key Parameters:
- $m = 2140$ kg (mass of Porsche Taycan Turbo)
- $C_d \cdot A = 0.513$ m² (drag-area product)
- $\rho = 1.293$ kg/m³ (air density)
- Max speed: 260 km/h
- Acceleration: 0–100 km/h in 3.2 s

#### Actuator Dynamics
To simulate a real-world response, a first-order actuator model with transfer function $\frac{1}{0.2s + 1}$ was added. However, the controller's model neglects this actuator dynamics and the slope $\theta$, testing its robustness against unmodeled dynamics and disturbances.

### MPC Implementation in MATLAB/Simulink
The MPC algorithm is implemented using a nonlinear MPC object (`nlmpc`) in MATLAB. The architecture in Simulink comprises:
- A Nonlinear MPC block
- Repeating sequence blocks for speed reference and slope disturbances ($\theta = 0^\circ$, $10^\circ$, $-10^\circ$)
- The Porsche Taycan dynamic model
- A unit delay block for feedback of the last control input

#### Tuning Parameters:
- Output variable weight: 1
- Manipulated variable weight: 0
- Manipulated variable rate of change weight: 0.002

### Results
The simulation demonstrates smooth control with minimal overshoot under varying slopes. However, a steady-state error is observed during uphill or downhill conditions, a common limitation of traditional MPC. Future work will focus on addressing this issue by making the controller "offset-free."

## Author
This project is developed by Simone Bertoni. Learn more about my work on my personal website - [Simone Bertoni - Control Lab](https://simonebertonilab.com/).

## Contact
For further communication, connect with me on [LinkedIn](https://www.linkedin.com/in/simone-bertoni-control-eng/).

