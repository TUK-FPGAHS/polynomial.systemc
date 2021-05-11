# SystemC Polynomial - Instructions

This file is part of the FPGAHS Lab from TU Kaiserslautern (TUK).
Author: Christian De Schryver



## Goals
After completing this lab, you should be able to...

* ... build a new SystemC module from scratch.
* ... implement a mathematical algorithm in SystemC.
* ... create a hierarchical SystemC module.
* ... implement a sequential module in SystemC.
* ... develop the test bench for a sequential module in SystemC.



## Setup
The template for this task is contained in the "polynomial.systemc" repository.

Please clone this repository to your working directory.
You will find template code for the given task and a file for the CMake build environment together with scripts for building and running the program.
In particular, execute...

* ... "./build.sh" to start the configuration and build process
* ... "./run<task>.sh" to execute the generated binary
* ... "./clean.sh" to remove all build artefacts located in the "cmakebuild" folder.



## Task Descriptions


### Task 1: Setup

1) Clone the "polynomial.systemc" repository to your working directory. Explore its contents and see where everything is located.
2) Execute "./build.sh" to check if the build environment is set up correctly.
3) Execute "./run-eval.sh". You should see the SystemC splash screen and some wrong results.


### Task 2: Polynomial Evaluation

1) Navigate to the "./src/polynom" folder and find the following files:
   * "poly.h" contains the polynomial evaluation module
   * "poly.cpp" contains implementation details for the module in "poly.h"
   * "stim_polynom.h" generates the stimuli for the test run
   * "mon_polynom.h" reads the stimuli and the output of the module and displays the results
   * "main.cpp" specifies the executable program that combines all modules to a complete simulation
2) Implement a functional module in "poly.h" and "poly.cpp" that calculates the value of a polynomial f(x) = sum (i=0, n, a_i * x^i) with a fixed degree and fixed coefficients a_i and variable x. Use the C-type "double" for arithmetic calculations.
   2a) Create a function in the file "poly.cpp" that implements the evaluation of the polynomial.
   2b) Create the module in "poly.h" that uses this function.
   2c) Integrate the module into the main function in "main.cpp".
3) Build and run the project with "./build.sh" and "./run-eval.sh". The correct output of your simulation should look like this:

>        SystemC 2.3.3-Accellera --- May 11 2021 09:18:18
>        Copyright (c) 1996-2018 by all Contributors,
>        ALL RIGHTS RESERVED
> 
> Correct result for X = -5
> Correct result for X = -4.9
> Correct result for X = -4.8
> […]
> Correct result for X = -0.3
> Correct result for X = -0.2
> Correct result for X = -0.1
> Correct result for X = 0
> Correct result for X = 0.1
> Correct result for X = 0.2
> […]
> Correct result for X = 4.6
> Correct result for X = 4.7
> Correct result for X = 4.8
> Correct result for X = 4.9
> 
> Info: /OSCI/SystemC: Simulation stopped by user.
   

## Task 3: Polynomial Integration

1) Navigate to the "./src" folder and find the following files:
   * "polyInt.h" contains the polynomial integration module
   * "polyInt.cpp" contains implementation details for the module in "polyInt.h"
   * "polyInt_tb.h" defines the testbench module
   * "polyInt_tb.spp" contains the implementation of the testbench
   * "main.cpp" specifies the executable program that combines all modules to a complete simulation
2) Provide a fully functional module in "polyInt.h" and "polyInt.cpp" that numerically approximates the definite integral of a polynomial. You can choose an integration algorithm that you like.
   2a) Specify a simple interface and communication protocol that includes control signals for transferring data between your module and the testbench.
   2b) Implement a sequential module using the module from Task 2 for the polynomial evaluation.
3) Create a testbench that verifies the correctness of the module implemented in 2).
   3a) Implement an algorithm that reliably calculates the correct result.
   3b) Use the specified protocol to create test stimuli for the module.
   3c) Retrieve the results from the module and compare them to the correct result.
   3d) Write the results of the test to the command-line.
4) Build and run the project with "./build.sh" and "./run-int.sh". Analyze the output manually and make sure the relative error is <10^-2. The output could e.g. look like this:

>        SystemC 2.3.3-Accellera --- May 11 2021 09:18:18
>        Copyright (c) 1996-2018 by all Contributors,
>        ALL RIGHTS RESERVED
> 
> 0 s Starting Test
> 
> 0 s Input set: -3 to 0
>  Calculated Result: 9.0135
>  Correct Result: 9
>  Relative Error: 0.0015005
>  after 10020 ns
> 
> 10020 ns Input set: -2 to 1
>  Calculated Result: 3.0075
>  Correct Result: 3
>  Relative Error: 0.0025015
>  after 20050 ns
> 
> 20050 ns Input set: -1 to 2
>  Calculated Result: 3.0075
>  Correct Result: 3
>  Relative Error: 0.0025015
>  after 30080 ns
> 
> 30090 ns Input set: 0 to -3
>  Calculated Result: -9.0135
>  Correct Result: -9
>  Relative Error: 0.0015005
>  after 40100 ns
> 
> 40110 ns Input set: -1 to -4
>  Calculated Result: -21.0225
>  Correct Result: -21
>  Relative Error: 0.00107164
>  after 50120 ns
> 
> 50130 ns Input set: -2 to -5
>  Calculated Result: -39.0315
>  Correct Result: -39
>  Relative Error: 0.000807808
>  after 60140 ns
> 
> Info: /OSCI/SystemC: Simulation stopped by user.



## Exam Questions
* What does the structure of a complex SystemC module look like?
* What are the advantages using SystemC in comparison to VHDL / Verilog / SystemVerilog?
* What is the difference between combinational and sequential modules?
* How are sequential designs described in SystemC?
* What is needed to transfer data between sequential modules?
