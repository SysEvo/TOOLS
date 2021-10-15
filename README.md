# TOOLS
General tools for gene regulatory circuits modeling.

## [GeneCircuit_Fit](https://github.com/SysEvo/TOOLS/tree/main/GeneCircuit_Fit)
ODE fitting pipeline for gene regulatory circuit models. Currently, it implements dynamic HMC algorithm (from [DynamicHMC.jl](https://github.com/tpapp/DynamicHMC.jl)) for fitting the model parameters.

_For Julia v.1.5.3_

* [Run_GeneCircuit_Fit.jl](https://github.com/SysEvo/TOOLS/blob/main/GeneCircuit_Fit/Run_GeneCircuit_Fit.jl): Instruction to run in julia terminal.
* [GeneCircuit_Fit.jl](https://github.com/SysEvo/TOOLS/blob/main/GeneCircuit_Fit/GeneCircuit_Fit.jl): Main pipeline to run fitting, reading user input files (i.e. InputFiles\\ARGS\_`iARG.mm`\_Par\_`iARG.ex`.jl, where `iARG.mm` and `iARG.ex` are the user provided labels for model file and parameters file, respectively), and generating the output file (i.e. OUT\_Fit\_`iARG.mm`\_`iARG.ex`.cvs, with labels as described above) with the posterior parameters and posterior σ from running Dynamic Hamilton Monte Carlo fitting for the parameters specified bye the user.
* [Library/FN_Fit.jl](https://github.com/SysEvo/TOOLS/blob/main/GeneCircuit_Fit/Library/Md_ToyEx1.jl): ODE simulations and other functions required to run GeneCircuit_Fit.jl.
* [Library/Md_ToyEx1.jl](https://github.com/SysEvo/TOOLS/blob/main/GeneCircuit_Fit/Library/Md_ToyEx1.jl): Example of model file. It must have the ODE set of the proposed model, one line for each variable, with `dX` representing the derivative function of the variable (i.e. species) `X`, and all variables starting with capital letters and all parameters starting with lowercase letters. For example, for the eauqtion `dY  = (mY * X) - (gY * Y)` representing the derivative of `Y`, `X`and `Y` are variables (i.e. species) and `mY` and `gY` are kinetic parameters.
* [InputFiles/ARGS_ToyEx1_Par_Ex01.jl](https://github.com/SysEvo/TOOLS/blob/main/GeneCircuit_Fit/InputFiles/ARGS_ToyEx1_Par_Ex01.jl): Example of input file. It must:
  * be **named** as InputFiles\\ARGS\_`iARG.mm`\_Par\_`iARG.ex`.jl, where `iARG.mm` and `iARG.ex` are the labels for model file and parameters file, respectively.
  * have the dictionary of **kinetic parameters** (`p`) and vector of **initial conditions** (`x0`).
  * include the **fitting instructions** (`pOp`), as a dictionary where each element correspond to a parameter to be fitted (with same notation than used in the kinetic parameters dictionaary `p`), and its value is a vector with the mean, standard deviation, minimum value, and maximum value for the fitting process.
  * specify the reference data, where `tD` are the time points, `vD` are the indexes to the observable variables in the model (i.e. the variables to be used for the fitting), and `xD` are the data points to compare with the model (array size: `vD` x `tD`).
