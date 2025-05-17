# Ocean Warming and Coastal Sea-Level Dynamics in California

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
Once the input files have been created, the model files can be transferred to the computing cluster. Begin by cloning a copy of [MITgcm](https://github.com/MITgcm/MITgcm) into your scratch directory and make a folder for the configuration, .e.g.

```bash
mkdir MITgcm/configurations/ocean_temperature_california
```

### Step 3: Compile the Model
Once all the files are on the computing cluster, the model cane be compiled. Make a ```build``` directory in the configuration directory and run the following lines:

```bash
../../../tools/genmake2 -of ../../../tools/build_options/darwin_amd64_gfortran -mods ../code -mpi
make depend
make
```
Then, use the ```scp``` command to send the ```code```, ```input```, and ```namelist``` directories to your configuration directory.
### Step 4: Run the Model 
After the compilation is complete, run the model with the wind. Move to the ```run``` directory, link everything from ```input``` and ```code```, and then submit the job script:

```bash
sbatch cs185c.slm
```

### Step 4.2 Run the Model with Warmed Theta
Next, run the model with the warmed theta ```Theta_warm_IC.bin```. Again, link everything from ```input``` and ```code``` to a directory called ```run_warmed```. Then, edit the ```data``` file to point to the modified files (see the Creating the Initial Conditions.ipynb). Then submit the job script again to rerun the model.

```bash
sbatch cs185c.slm
```

### Step 4.3 Run the Model with Cooled Theta
Next, run the model with the cooled theta ```Theta_cool_IC.bin```. Again, link everything from ```input``` and ```code``` to a directory called ```run_cooled```. Then, edit the ```data``` file to point to the modified files (see the Creating the Initial Conditions.ipynb). Then submit the job script again to rerun the model.

```bash
sbatch cs185c.slm
```

### Step 5: Analyze the Results
There are two notebooks provided for analysis:
   1. Analyzing the Model Results

      This notebook is provided to have a quick look at spatial and temporal variations in the temperature field in the model with both warmed 
      and cooled Theta fields with +/- 2°C changes. It also generates the visualization provided in the figures directory.
   3. Answering the Science Question
    
      This notebook provided some analysis plots to address the science question posed above.  
