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


# VIonLDA

This package includes:

### 1 Main Functions 

* simulation_data()

Data simulation based on LDA model, the output is a list of one-hot-coding matrices.

* M_step_Vectorization()

Vectorized version of Variational EM algorithm on LDA. Requires the function E_step_Vectorization().

* M_step_Smoothing()

Vectorized version of Variational EM algorithm on smoothing LDA. Requires the function E_step_Smoothing(). 

* mmse()

Evaluation function.

### 2 Other functions 

* M_step_Plain()

Naive version Variational EM algorithm on LDA. Requires the function E_step_Plain().

* M_step_Structure()

Structured version of Variational EM algorithm on LDA. Requires the function E_step_Structure(). This algorithm is based on the vectorized version, though in E step it takes vector as input.

* M_step_Realdata()

To avoid overflow when applied in real dataset, set the float128 as the data type. A slightly change on the vectorized version. Requires the function E_step_Realdata()

# Tests

Inside is a .ipynb file showing how to apply these functions and reproduce the result on simulation data in the report. 

# Examples

Inside is a .ipynb file showing how to apply these functions to real datasets and reproduce the result in the report.

# Parallel

Inside is a .ipynb file showing the parallel version of Variational EM on LDA. Make sure you $pip install ray before run it. Sometimes ray cannot run in the Virtual Machine (VM). If this happens please restart the VM. Since Parallel version does not always work (depends on the condition of the computer), we have decided to exclude this part from the package.

# Ideal Data Structure But Poor Performance

As we mentioned in the discussion, we designed a version of ideal data structure. We implemented matrix multiplicaiton, vectorization and broadcast in this version. The speed is much faster: We can see with the same initialization (10 times iteration), this version takes only half of the time needed by the vectorization version in the report. However, the mse is worse than the vectorization version.

# Notice

- All the defaults of the function are set as the report suggests. 

- To reproduce the result in the report, use random seed 123.

- See lda_ideal_data_structure_worse_behavior.ipynb for further discussion about an theoretically better data structure. For the poor performance in reality, we do not include this part in our package and report. But it is worth discussing. 
