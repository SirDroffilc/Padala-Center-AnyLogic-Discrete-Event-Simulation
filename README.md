# Mabuhay Padala Center - AnyLogic Discrete Event Simulation

## Overview
This repository contains an AnyLogic Discrete Event Simulation (DES) model of the **Mabuhay Padala Center**. The simulation models the end-to-end operational flow of a logistics and package delivery hub, from customer arrival and order processing to internal warehouse handling, and finally, outbound truck dispatch.

By adjusting parameters such as customer arrival rates, employee counts, and truck dispatch limits, this model allows for robust sensitivity analysis to identify bottlenecks and optimize the facility's performance.

## System Components
1. **Inbound & Processing:** Simulates the customer journey (arrival, queuing, service) and the transformation of digital orders into physical packages processed by warehouse staff.
2. **Storage & Outbound Logistics:** Models the internal handling of boxes, floor storage capacity dynamics, and a pull-based truck dispatch system that dynamically responds to warehouse volume.
3. **Performance Metrics:** Tracks comprehensive statistics including turn-around times (for customers, packages, and trucks) and resource utilization (Customer Service and Manual Labor employees).

## Visualizations

### 1. 3D View
<!-- Replace the link below with the actual path to your 3D view screenshot -->
![3D View](https://github.com/SirDroffilc/Padala-Center-AnyLogic-Discrete-Event-Simulation/blob/master/sample_simulation_images/padala_3d.png?raw=true)

### 2. 2D View
<!-- Replace the link below with the actual path to your 2D view screenshot -->
![2D View](https://github.com/SirDroffilc/Padala-Center-AnyLogic-Discrete-Event-Simulation/blob/master/sample_simulation_images/padala_2d.png?raw=true)

### 3. Statistics
<!-- Replace the link below with the actual path to your statistics screenshot -->
![Statistics](https://github.com/SirDroffilc/Padala-Center-AnyLogic-Discrete-Event-Simulation/blob/master/sample_simulation_images/padala_statistics.png?raw=true)

### 4. Logic Flow
<!-- Replace the link below with the actual path to your logic flow screenshot -->
![Logic Flow](https://github.com/SirDroffilc/Padala-Center-AnyLogic-Discrete-Event-Simulation/blob/master/sample_simulation_images/padala_logic.png?raw=true)

## How to Run the Simulation

To run this simulation model on your local machine, follow these steps:

1. **Download AnyLogic PLE:**
   - Go to the [AnyLogic Download Page](https://www.anylogic.com/downloads/).
   - Download and install the **AnyLogic Personal Learning Edition (PLE)**, which is free for educational and self-learning purposes.

2. **Get the Model:**
   - Clone this repository or download it as a ZIP file to your computer.

3. **Open the Model:**
   - Launch AnyLogic PLE.
   - Click on **File > Open...** (or the Open icon in the toolbar).
   - Navigate to the folder where you downloaded this repository.
   - Select the MPCR_Simulation.alp file and open it.

4. **Run the Simulation:**
   - In the AnyLogic workspace, look for the **Projects** view (usually located on the left panel).
   - Expand the MPCR_Simulation project tree if it isn't already expanded.
   - Find and right-click on **Simulation: Main** under the Simulation experiment.
   - Select **Run** from the context menu (or select it and click the green Play button in the top toolbar).
   - A new simulation window will launch. Click the **Play** button at the bottom of the window to start the execution and observe the model.
