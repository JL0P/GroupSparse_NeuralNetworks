# Regularised neural network for burst detection and localization In Water Distribution Networks
This repository contains a collection of MATLAB and Python scripts for EPANET-based dataset generation, neural network tuning (network structure + regularization), and sensor pruning based on learned weights. The workflow is divided into steps, each with its own script/notebook, as discussed in my thesis[1] and in [2].
The workflow is divided into steps, each with its own script/notebook. Below is an overview of how to set up and run them.

## References
[1] **Lo Presti, J.**. "Neural Network-Based Methods for the Management and Control of Complex Systems." (2025).

[2] **Lo Presti, J., et al.** (2024). *Combining clustering and regularised neural network for burst detection and localization and flow/pressure sensor placement in water distribution networks.* Journal of Water Process Engineering, **63**, 105473.

# Scripts Overview
1. Dataset Generation & Splitting:

The data used in this repository cannot be publicly shared due to confidentiality constraints. However, the same methodology applies to *any* Water Distribution Network. By simulating an EPANET model (see [1,2] for guidelines), you can generate similar data to train and test your models.

This step involves:
- Generating synthetic or real data from an EPANET simulation.
- Organizing the resulting data into Train, Validation, and Test sets.

2. Network Structure Tuning

        tuning_net_structure.py
    
    Uses Python’s Keras Tuner to optimize neural net architecture (e.g., layer sizes, learning rate) with Val1.
    The results, including logs and hyperparameter grids, are saved in INFO/ subfolders.

3. L21 Regularization Tuning

        tuning_L21.py

    Focuses on tuning the L21 (group-sparse) regularization hyperparameter. Trains on Train+Val1 and checks performance on Val2.

4. Pruning Sensors via Norm2 & Retraining

A key MATLAB scripts plus corresponding Python evaluation scripts:

    allModelsThAndGridEvaluation.m

applies norm-2 thresholds to input weights to decide which sensors to keep and calling 

        evaluateModelAtDifferentTh.py

a Python function invoked by the MATLAB script to evaluate the model across thresholds.

5. Final Single-Threshold Pruning

Once the threshold is fixed, re-train from optimized weights, again using Train+Val1 / Val2 using 

    allModelsThAndGridEvaluation_singleTh.m

which calls 

      evaluateModelAtSingleTh.py

for fine-tuning the final models.

>**Note:** This code is provided as a demonstrative scratch to show the core concepts and workflow. Non-essential functions and details have been omitted for brevity. If you need additional information or the missing parts, feel free to contact me or open an issue – I’ll be happy to assist!

