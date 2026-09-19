# Modeling of Three-Phase Inverter Using MATLAB/Simulink

## Overview

This project implements the **modeling and simulation of a three-phase inverter using MATLAB/Simulink**. The Simulink model generates the inverter switching signals, while a MATLAB script processes the simulation data and provides a graphical animation of the three-phase switching states and rotating vector.

The project helps visualize how the switching states of a three-phase inverter change as the electrical angle varies.

## Features

* Three-phase inverter modeling using **Simulink**
* MATLAB-based simulation control
* Visualization of phases **A, B, and C**
* Representation of the three phases with **120° phase displacement**
* Extraction of switching states from Simulink using `logsout`
* Dynamic visualization of inverter switching combinations
* Rotating vector animation based on the simulated electrical angle
* Color-based indication of active switching states
* Automatic animation over the complete simulated dataset

## Software Requirements

* MATLAB
* Simulink
* Simscape Electrical / required electrical modeling libraries, depending on the blocks used in the Simulink model

## Project Model

The MATLAB script opens and simulates the Simulink model:

```matlab
mdl = 'Modeling_three_phase_inverter';

open_system(mdl);
sim(mdl);
```

The simulation results are obtained through the `logsout` object.

The script expects:

```matlab
logsout{1}
```

to contain the **electrical/rotor angle in degrees**, and

```matlab
logsout{2}
```

to contain the **six inverter switching signals**.

## Three-Phase Representation

The three phases are positioned 120° apart:

```text
Phase A =    0°
Phase B =  120°
Phase C = -120°
```

This creates the basic three-phase spatial representation used in the animation.

Conceptually:

```text
                 B
                /
               /
              ●
             /
            O──────── A
             \
              \
               ●
                \
                 C
```

where `O` represents the center of the three-phase system.

## Switching States

The six switching signals obtained from the Simulink model are used to determine which inverter switches are active.

The MATLAB program recognizes switching combinations such as:

```matlab
[1 0 0 0 0 1]
[0 0 1 0 0 1]
[0 1 1 0 0 0]
[0 1 0 0 1 0]
[0 0 0 1 1 0]
[1 0 0 1 0 0]
```

Each switching pattern corresponds to a particular inverter state.

The phase markers are dynamically updated using different colors to indicate the corresponding switching condition.

## Rotating Vector Animation

The simulated angular position is converted from degrees to radians:

```matlab
ro = ro1(l)*pi/180;
```

The rotating vector coordinates are then calculated using:

```matlab
xr1 = l1*cos(ro);
yr1 = l1*sin(ro);

xr2 = -l1*cos(ro);
yr2 = -l1*sin(ro);
```

This creates a line passing through the origin whose orientation changes according to the simulated angle.

The graphical objects are updated using:

```matlab
set(hl1,'XData',[xr1 xr2]);
set(hl1,'YData',[yr1 yr2]);
```

and MATLAB's

```matlab
drawnow
```

command produces the animation.

## Working Flow

```text
Start
  |
  v
Open Simulink Model
  |
  v
Run Three-Phase Inverter Simulation
  |
  v
Collect Simulation Data using logsout
  |
  +----------------------+
  |                      |
  v                      v
Electrical Angle     Switching Signals
  |                      |
  v                      v
Convert Degree       Identify Current
to Radian            Switching State
  |                      |
  v                      v
Calculate Vector     Update A/B/C
Coordinates          Marker Colors
  |                      |
  +----------+-----------+
             |
             v
       Update Plot
             |
             v
          drawnow
             |
             v
      Repeat for Data
             |
             v
            End
```

## Output

The MATLAB animation displays:

* A circular three-phase reference diagram
* Phase points **A, B, and C**
* Active inverter switching states
* A rotating vector representing the simulated angular position
* Continuous graphical updates according to the Simulink output

## Applications

This project can be useful for understanding:

* Three-phase voltage-source inverters
* Power-electronic switching
* Three-phase switching sequences
* Electrical angle representation
* Inverter control techniques
* Space-vector concepts
* Motor-drive inverter operation
* MATLAB/Simulink-based power electronics simulation

## Project Structure

```text
Three-Phase-Inverter/
│
├── Modeling_three_phase_inverter.slx
├── inverter_animation.m
└── README.md
```

The `.slx` file contains the inverter simulation model, while the MATLAB script runs the simulation and generates the switching-state animation.

## Conclusion

The project demonstrates the **simulation and visualization of a three-phase inverter using MATLAB and Simulink**. Simulink performs the inverter simulation and generates the switching and angular data, while MATLAB processes these signals to dynamically visualize the phase switching states and rotating electrical vector.
