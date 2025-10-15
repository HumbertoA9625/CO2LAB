CO₂ Injection Simulation using MRST

This repository contains a simplified workflow for simulating CO₂ injection using the Matlab Reservoir Simulation Toolbox (MRST).
The setup is inspired by the FluidFlower experimental configuration and demonstrates how to go from an experimental setup to a computational mesh and a full black-oil simulation.

📂 Repository Structure

experiment_to_mesh/
Contains figures illustrating how to transition from the experimental setup to the computational grid. These examples are derived directly from the FluidFlower medium.

mrstExample/
Includes the main MATLAB scripts and input files for the simulation.
The primary script is exampleCO2inj, which is thoroughly commented and also available as a .mlx file for better visualization within MATLAB.

⚠️ The mesh generation code is not included in this repository.

🧠 About MRST Core Module

The MRST core module provides essential data structures and routines for reservoir modeling, including:

Geological description: structured and unstructured grids

Petrophysical properties (porosity, permeability, net-to-gross, etc.)

Drive mechanisms (wells, boundary conditions)

Reservoir state (pressures, saturations, fluxes, etc.)

It also includes:

Numerous grid-factory routines and transmissibility calculations

A library for automatic differentiation (optimized for sparse matrices and coupled PDEs)

Tools for plotting cell and face data

Built-in physical units and conversion utilities

Routines for reading and writing ECLIPSE input data

To explore available examples in MATLAB:

>> mrstExamples


To list examples for a specific module, e.g. ad-core:

>> mrstExamples ad-core

🚀 How to Run the Simulation
Requirements

MATLAB (R2022a or later recommended)

MRST 2022a — Download here

Required MRST modules:
upr, ad-props, ad-blackoil, deckformat, ad-core, mrst-gui, linearsolvers
---------------------------------------------------------------------------
Steps


Open MATLAB

Run the startup.m file located in your MRST folder

Change the path to the folder

Run the script exampleCO2inj.m

The first time you run the model, MATLAB will prompt you to download and set up AMGCL and Boost.
Simply click “OK” — MRST handles this automatically.
These libraries significantly improve performance for large and fine-mesh models.

----------------------------------------------------------------------------------------
🧩 Model Components
1. Mesh

Predefined meshes (coarse or fine) are loaded from the provided directory.
Each region (reservoir, caprock, fault) is color-coded for visualization.

2. Rock Properties

Porosity and permeability are assigned per region.
Values differ depending on the simulation depth (surface or 1km).

3. Fluids

Fluid properties are initialized from ECLIPSE-type .DATA files, including:

Formation volume factors (FVF)

Capillary pressure

Relative permeability

Compressibility and surface densities

Thermodynamic models follow formulations from:

Duan & Sun (2003), Chemical Geology

Spycher et al. (2003), Geochimica et Cosmochimica Acta

Hassanzadeh et al. (2008), IJGGC

4. Initialization

Hydrostatic pressure distribution and initial saturations are computed numerically, assuming full water saturation.

5. Wells

Injection wells are defined with variable injection rates, depth options, and total simulation times (ranging from minutes to years, depending on the case).

6. Model Setup

The GenericBlackOilModel is configured with adaptive nonlinear solvers (CPR preconditioning, line search, timestep strategy).

7. Boundary Conditions

For surface cases: constant pressure on top faces

For 1 km depth cases: no-flow boundaries with open aquifer approximation

8. Schedule

Injection schedules include ramp-up, constant injection, and ramp-down phases.

9. Simulation Execution

Simulations are packaged and executed using:

[ok, status] = simulatePackedProblem(problem);


All outputs — reports, states, and well solutions — are saved automatically to the directory defined in outputDir.


10. Results & Visualization

Post-processing includes pressure evolution, saturation fronts, and 3D visualizations
