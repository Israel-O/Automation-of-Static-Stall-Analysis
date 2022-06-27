# Automation-of-Static-Stall-Analysis
**NACA Image**
An attempt to develop a script to automate the analysis of any airfoil profile led to the demonstration of the idea of using a data container application as a mediator between simulation and postprocessing software. This project uses Fluent to measure the forces acting on an Airfoil Profile and sends the data to excel and then to MATLAB where the numbers are automatically processed and a summary is made. Report files and images are also automatically produced for the user's benefit. The code is written in Python and MATLAB and its purpose is to identify the critical angle of attack. This idea can be scaled to help developers come up with personalized optimization algorithms for control surfaces or complex parameterization that might require machine learning.

### Glosary
- **Static Stall**: An occurrence when the airflow around a lifting body separates, till its net lift produced is less than zero.
- **AOA (Angle of Attack)**: The angle at which the chord of an aircraft’s wing meets the relative wind
- **NACA 4412**: Cross-section of the wing of an aircraft

### Demonstartion

**sim video**

### Workbench Project Schematic
**Image**

### Mesh Setup
**Mesh Image**

Mesh Nodes: 161,678 nodes
Mesh Elements: 320,221 elements

**Image**
**Image**
- All triangles method
- Edge Sizing
- Inflation layer

### Fluent Setup
Pressure-Based Solver
Space: 2D
Time: Unsteady, 2nd-Order Implicit
Material: air (Fluid)
Turbulence Model: SST k-Ω model

**Image**

### Boundary Conditions
Velocity-inlet (m/s): Parameter 6 - V_in
Pressure-outlet (Pa): 0 Pa

**Image**

### Process Flowchart

**Image**

### Proposed Applications
- Design automation
- Complex parameterization
- Personal optimization algorithms
- Machine learning
- Generative design
- Rapid postprocessing
