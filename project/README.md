# California Upwelling

In this project, I will investigate the effects of ocean temperature and how it affects the California sea level. 

## Scientific Question

How does ocean temperature affect the sea level along the coast of California?

## Project Description

To investigate, I will research how ocean temperature affects the sea level along the coast of California. Specifically, I will look into thermal expansion and density variations and how they influence sea level. To do this, I will analyze fields such as salinity (SALT), temperature (THETA), sea level, and depth (Bathymetry). For the initial conditions, I will use ECCO Version 5 model to obtain the salinity and temperature data. To further investigate this question, I will use MITgcm as the numerical ocean model to simulate the sea level change to see the response to ocean temperature variation. I will calculate the sea level change by analyzing the change in density caused by ocean temperature. To analyze the results I will use a timeseries to show the changes over time. To visualize the results I will create a movie that will demonstrate the difference between a varying temperature field and a fixed field.

## Project Description
The following steps can be used to construct the model files, configure and run the model, and assess the model results:

### Step 1: Create the Model Files
Several input files are needed to run the model. Generate the following list of files using the notebooks (indicated in the parentheses):

* Model Grid (notebooks/Creating the Model Grid.ipynb)
* Bathymetry (notebooks/Creating the Bathymetry.ipynb)
* Initial Conditions (notebooks/Creating the Initial Conditions.ipynb)
    * This is important as you will get three Theta files along with the other initial conditions
* External Forcing Conditions (notebooks/Creating the External Forcing Conditions.ipynb)
* Boundary Conditions (notebooks/Creating the Boundary Conditions.ipynb) The model files should be placed into the input 
  directory.

### Step 2: Add files to the Computing Cluster
Once the input files have been created, the model files can be transferred to the computing cluster. Begin by cloning a copy of MITgcm into your scratch directory and make a folder for the configuration, .e.g.

mkdir MITgcm/configurations/ocean_temperature_california

### Step 3: Compile the Model
Once all the files are on the computing cluster, the model cane be compiled. Make a build directory in the configuration directory and run the following lines:
../../../tools/genmake2 -of ../../../tools/build_options/darwin_amd64_gfortran -mods ../code -mpi
make depend
make

### Step 4: Run the model 
After the compilation is complete, run the model with the wind. Move to the run directory, link everything from input and code, and the submit the job script:

```bash
sbatch cs185c.slm
```
