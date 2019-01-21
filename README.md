# VIonLDA

Created by: Yunran Chen, Junwen Huang

This project is the application of Variational Inference on Latent Dirichlet Allocation. We mainly reproduced paper by Blei et al. 2003. There are three main parts: 

* Functions packaged inside package VIonLDA, which includes all the versions of functions mentioned in the report. These functions cover data simulation, Variational EM algorithm on LDA and smoothing LDA. 

* All the simulations mentioned in the report. 

* A real-world application.

Here since the parallel version does not always work, we exclude it from our package.

# Install the package

* Please make sure the package version is 2.7. 

%%bash

pip install --index-url https://test.pypi.org/simple/VIonLDA

To install the latest version, first uninstall:

pip uninstall --index-url https://test.pypi.org/simple/VIonLDA

Then install the latest version:

%%bash

pip install -I --index-url https://test.pypi.org/simple/VIonLDA


# Functions inside package VIonLDA

This package includes:

## Main Functions 

* simulation_data()

Data simulation based on LDA model, the output is a list of one-hot-coding matrices.

* M_step_Vectorization()

Vectorized version of Variational EM algorithm on LDA. Requires the function E_step_Vectorization().

* M_step_Smoothing()

Vectorized version of Variational EM algorithm on smoothing LDA. Requires the function E_step_Smoothing(). 

* mmse()

Evaluation function.

## Other functions 

* M_step_Plain()

Naive version Variational EM algorithm on LDA. Requires the function E_step_Plain().

* M_step_Structure()

Structured version of Variational EM algorithm on LDA. Requires the function E_step_Structure(). This algorithm is based on the vectorized version, though in E step it takes vector as input.

* M_step_Realdata()

To avoid overflow when applied in real dataset, set the float128 as the data type. A slightly change on the vectorized version. Requires the function E_step_Realdata()

# Tests

Inside is .ipynb showing how to use this functions and reproduce the result on simulation data in the report. 

# Examples

Inside is .ipynb showing how to use these functions on real datasets and reproduce the result in the report.

# Parallel

Inside is .ipynb showing the parallel version of Variational EM on LDA. Make sure you $pip install ray before run it. Sometimes ray cannot run in VM. Please restart the VM. Because Parallel version would not always work. Depends on the condition of your computer. We decide to exclude this part from the package.

# Notice

- All the defaults of the function are set as the report suggest. 

- To reproduce our result, do include random seed 123.

- We expand more on the discussion in our report to firgure out a better data structure. See lda_ideal_data_structure_worse_behavior.ipynb. For the poor behavior, we do not include this part in our package and report. But it is worth discussing.

# Ideal Data Structure But Poor Behavior

As we mentioned in the discussion, we design a version for ideal data structure. We implemented matrix multiplicaiton, vectorization and broadcast in this version. We can see the speed is super fast. However, the core idea that VI work is the Variational parameter $\phi$, $\gamma$ converge. (make the KL distance as small as possible to approximate the probability density) So if we break this rule, the algorithm cannot converge and even intractable. We can see with the same initialization, 10 times iteration, the time for this algorithm is only half of the vectorization version we adopt in the report. However, the mse is a factor of 0.1 to 0.01 in scale worse than the vectorization version. 

 
