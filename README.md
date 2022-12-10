# Traffic Simulation Project
In the following, code execution instructions are given to comprehend the results achieved in the lecture "Simulation and Optimization". Please see the descriptions of the special cases below before running a simulation or an optimization experiment.

## Code structure
Generally, the code is structured in several folders. Class definitions of controllers, optimizers or additionals like TrafficLight or Lane can be found in the corresponding top-level folder. The configuration, flow, routes, etc. files, definitions of evaluation functions and experiment or optimization runners can be found in the folders "arterial" or "GridNetwork" dependent on which network is considered. The folder "additionalFuncs" contains the definitions of evaluation function and helper functions. "Experiments" contains files to execute single simulation runs for the controllers. In "LPSolve" one finds LPSolve results used for generating the correct traffic loads for the cycle based approaches. In the folder "Optimization" files for running optimization experiments with different controllers are stored. 

## Perform a single simulation run on the 1x5 arterial network
To perform a simulation run with a specific controller, the simulation settings must be set in the corresponding file. For example, to run a simluation for AdaSOTL on the arterial network, open the file "arterialRunnerAdaSOTL.py in the folder "arterial/Experiments". 
* Change parameters like numVehicles or hyperparameters like alpha and beta as needed. 
* Set parameter called "delta_r_t" of the function setFlows_arterial correctly to control the turn probabilities. 
* Change the flow file path to "arterial.flow_delta_r_t_0.xml" for delta_r_t = 0 in the runner file as well as in the config file "arterial.jtrrcfg".
* Make sure to start in the correct folder

Example:
```
cd arterial/Experiments
python arterialRunnerAdaSOTL.py
```

## Perform an optimization run on the 1x5 arterial network
* Change hyperparameters of simulation and optimizer (see implementations in folder "optimizers")
* Create new folder in the folder "arterial/Plots" and change the path in the optimization script to save resulting plots and data
* Set parameter called "delta_r_t" of the function setFlows_arterial correctly to control the turn probabilities. 
* Change the flow file path to "arterial.flow_delta_r_t_0.xml" for delta_r_t = 0 in the runner file as well as in "arterial/additionalFuncs/evaluation.py"
* Make sure to start in the correct folder

Example:
```
cd arterial/Optimization
python arterialHillClimbing_AdaSOTL.py
```

## Perform a single simulation run on the 2x3 grid network
* Change parameters like numVehicles or hyperparameters like alpha and beta as needed. 
* Change the flow file path to "2x3.flow_fixed.xml" in the runner and in the config file "2x3.jtrrcfg" to fix flow (a) and therefore stop flow switching.
* Make sure to start in the correct folder

Example:
```
cd GridNetwork/Experiments
python 2x3RunnerAdaSOTL.py
```

## Perform an optimization run on the 2x3 grid network
* Change hyperparameters of simulation and optimizer (see implementations in folder "optimizers")
* Create new folder in the folder "GridNetwork/Plots" and change the path in the optimization script to save resulting plots and data
* Change the flow file path to "2x3.flow_fixed.xml" for fixed flows in the runner file as well as in "GridNetwork/additionalFuncs/evaluation.py"
* Make sure to start in the correct folder

Example:
```
cd GridNetwork/Optimization
python 2x3HillClimbing_AdaSOTL.py
```

## Special instructions for cycle based (CB) approach
To run a simulation or an optimization with the cycle based controller, please note additionally:
* Change the "lpSolveResultPaths" to the correct values of considered epsilon or turn probabilities in the runner script for single simulation runs or in "arterial/additionalFuncs/evaluation.py" / "GridNetwork/additionalFuncs/evaluation.py" for optimization experiments
  * 1x5 arterial network:
    * In case delta_r_t = 0: ['../LPSolve/arterial_a_eps0,2.lp.csv', '../LPSolve/arterial_a_eps0,2.lp.csv', '../LPSolve/arterial_a_eps0,2.lp.csv']
    * In case delta_r_t = 1/16: ['../LPSolve/arterial_a_eps0,2.lp.csv', '../LPSolve/arterial_b_eps0,2.lp.csv', '../LPSolve/arterial_c_eps0,2.lp.csv']
    * In case delta_r_t = 2/16: ['../LPSolve/arterial_a_eps0,2.lp.csv', '../LPSolve/arterial_c_eps0,2.lp.csv', '../LPSolve/arterial_d_eps0,2.lp.csv']
  * 2x3 grid network:
    * In case numVehicles = 900: ['../LPSolve/2x3Grid_a_eps0,4.lp.csv', '../LPSolve/2x3Grid_b_eps0,4.lp.csv', '../LPSolve/2x3Grid_c_eps0,4.lp.csv']
    * In case numVehicles = 1200: ['../LPSolve/2x3Grid_a_eps0,2.lp.csv', '../LPSolve/2x3Grid_b_eps0,2.lp.csv', '../LPSolve/2x3Grid_c_eps0,2.lp.csv']
    * In case numVehicles = 1500: ['../LPSolve/2x3Grid_a_eps0,1.lp.csv', '../LPSolve/2x3Grid_b_eps0,1.lp.csv', '../LPSolve/2x3Grid_c_eps0,1.lp.csv']
  * 2x3 grid network fixed flow:
    * In case numVehicles = 900: ['../LPSolve/2x3Grid_a_eps0,4.lp.csv', '../LPSolve/2x3Grid_a_eps0,4.lp.csv', '../LPSolve/2x3Grid_a_eps0,4.lp.csv']
    * In case numVehicles = 1200: ['../LPSolve/2x3Grid_a_eps0,2.lp.csv', '../LPSolve/2x3Grid_a_eps0,2.lp.csv', '../LPSolve/2x3Grid_a_eps0,2.lp.csv']
    * In case numVehicles = 1500: ['../LPSolve/2x3Grid_a_eps0,1.lp.csv', '../LPSolve/2x3Grid_a_eps0,1.lp.csv', '../LPSolve/2x3Grid_c_eps0,1.lp.csv']

## More resources
More information on the project is found in our <a href="https://github.com/bentecus/AdaSOTL/blob/main/docs/Technical_Report_AdaSOTL.pdf">technical report</a> concerning the project as well as the gained results.

## About
Contributors: Marcus Bentele, Georg Fessler, Thomas Rosenberger

This repository was created during a project in Simulation and Optimization taking place during the 3. Semester Master Informatis at FH Voralberg University of Applied Sciences.