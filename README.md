# HPC-A
## Numerical Simulation and Visualization of 2D Rayleigh--Bénard Convection
This project is a simulation software for 2D Rayleigh--Bénard Convection. The software takes the input
from user interface, uses numerical solver to compute the temperature and velocity field of fluids,
simulates and visualizes the results of computation, and displays results in a graphical user interface.

## Group Members
Yang Jiao, Yiming Li, Kit Sum Wu  

## Design Philosophy
Our project is divided as three parts: numerical calculation and simulation of Rayleigh--B\'enard Convection in 2D space, data visualization of simulation and GUI design. In our project, we need to solve a constitute equations for Rayleigh--B\'enard Convection and  build a 2D mesh simulation with parameters, including fluid properties, fluid volume geometry, time step,mesh spacing and simulation duration. The simulation will produce fluid velocity and temperature for each mesh node for data visualization. However, problems like converge failure, low simulation speed and are needed to be pay attention to.
 
The input of data visualization is the result of Rayleigh--B\'enard Convection simulation and the resulting graphics should be exported to GUI section. It gives users a direct view of their calculation and help them to better understand Rayleigh--B\'enard Convection or the errors occurred in their calculation. The configurations should include output map layer, dimensions of output, color schemes and result export format. The main challenges can be the data format of the integration and the computational efficiency.
 
Graphical User Interface is like a conductor of the project. It control the progress of both simulation and visualization. There should be four main functions in GUI: data loading and saving, parameter setting, progress control like start or pause and result display. However, we may encounter challenges like processing large data set, dealing the data concurrency and the warning of invalid input or errors in the simulation and visualization.

## Build instructions
### Simulation: Getting started with openFOAM
This section provides instructions for running openFOAM simulations on the Brown CCV Linux Redhat environment. First, the following commands should be entered into the terminal to load modules which are necessary for the project:

`module load mpi/openmpi_2.0.3_intel`
`module load openfoam/4.1`

Then, the following command should be run:

`source $FOAM_INST_DIR/OpenFOAM-4.1/etc/bashrc`

If this is the first time you are using openFOAM, you must make a copy of the openFOAM tutorial files which you have permission to edit. To do this, we use the following command to create a destination directory to which we will copy the tutorial files:

`mkdir -p $FOAM_RUN`

We then copy the files from the tutorials directory in the openFOAM file set to this newly created directory:

`cp -r $FOAM_TUTORIALS $FOAM_RUN`

If you have already done this step, there is no need to repeat it.

### Simulation: Setting up the simulation
In OpenFOAM, the details of a simulation are included in what is called a case directory. The version of openFOAM available on the Brown CCV, openFOAM 4.1, does not have a case directory for Rayleigh Benard convection, so we will create our own. First, navigate to the solver directory:

'cd $FOAM_RUN/tutorials/heatTransfer/bouyantBoussinesqPimpleFoam/'

You can download the case directory from this Github repository, which is based off of the guide on [CuriosityFluids](https://curiosityfluids.com/2017/06/12/rayleigh-benard-convection-using-buoyantboussinesqpimplefoam/). This case directory models a 2D flow in a rectangular region. Alternatively, you can download and modify the case directory for Rayleigh-Benard Convection [here](https://github.com/OpenFOAM/OpenFOAM-6/tree/master/tutorials/heatTransfer/buoyantBoussinesqPimpleFoam/BernardCells), which is set up to model 3D convection. The files included in this directory and their purpose are described here. To begin with, the case directory contains subdirectories titled '0', 'constant', and 'system' directories. The '0' directory contains files describing the initial conditions. The 'constant' directory contains information on physical constants and properties of the fluid. The 'system' directory contains directions for setting up the simulation. The case directory will also contain time directories corresponding to time steps in the simulation once the solver has been run. These directories contain the results of the simulation at each time step. A file tree of the case directory is shown below.

```bash
├── 0
│   ├── p
│   ├── p_rgh
│   ├── T
│   ├── U
│   ├── alphat
├── constant
│   ├── g
│   ├── transportProperties
│   ├── turbulenceProperties
├── system
│   ├── blockMeshDict
│   ├── controlDict
│   ├── fvSolution
│   ├── fvSchemes
├── Time Directories
```

#### 1. Create Mesh
Information regarding how to specify the geometry of a mesh can be found on the [OpenFOAM User Guide](https://cfd.direct/openfoam/user-guide/v4-mesh-description/).


Once you are finished editing the file 'blockMeshDict', create the mesh by entering the following command in the case directory:

'blockMesh'

#### 2. Set Boundary and Initial Conditions
Initial conditions can be changed by accessing the '0' folder from the case directory and changing the parameters contained in the files there.

#### 3. Set Physical Properties
From the case directory, navigate to the system folder:

'cd constant'

Then, open the file 'transportProperties' in your text editor of choice and edit the fields "nu", "beta", "TRef", and "Pr" as desired.
#### 4. Set Simulation options
From the case directory, navigate to the system folder:

'cd system'

Then, open the file 'controlDict' in your text editor of choice and edit the fields "startTime", "endTime", "deltaT", and "writeInterval" as desired.

#### 5. Run the application
Enter the following text in the command line from the case directory:

'bouyantBoussinesqPimpleFoam'

### Simulation: Saving data and loading data
#### Postprocessing

## References
https://openfoamwiki.net/index.php/FAQ/Installation_and_Running

https://canvas.vt.edu/files/4773672/download?download_frd=1

https://www.openfoam.com/documentation/tutorial-guide/tutorialse2.php#x6-60002.1

https://cfd.direct/openfoam/user-guide-v4/

http://www.hpc.lsu.edu/training/weekly-materials/2014-Fall/intro_of_20141105.pdf

