# PARAMETERIZED QUANTUM CIRCUIT AS MACHINE LEARNING MODEL (Make-Moons Dataset)

This project implements a binary quantum classifier using a Parameterized Quantum Circuit
(PQC) built with Qiskit 2.0.

The model uses:

- A custom encoder circuit to embed classical 2-D data into quantum states
- A variational circuit with trainable parameters
- The Estimator primitive to compute expectation values
- Classical optimization (COBYLA) to train the quantum model
- Make-Moons synthetic dataset for nonlinear binary classification

## Project Overview

The workflow includes:

1. Dataset Preparation
    o Generate a 2-class nonlinear dataset using make_moons
    o Standardize and split into train/test sets
2. Quantum Feature Encoder
    Encodes 2-D input features into rotations and entanglement using:
       o RY rotations
       o CX entanglement
       o Additional nonlinear embedding via RZ(x₀·x₁)
3. Variational Quantum Circuit
    A trainable 2-qubit Ansatz with four parameters:
       o Rotations (RY)
       o Entangling layer (CX)
       o Second rotation layer
       o Second entangling layer
4. Estimator-based Measurement
    Uses the observable Z ⊗ I
    Maps expectation values → probabilities via: 𝑝(𝑦= 1 ∣𝑥)=(⟨𝑍𝐼⟩+ 1)/ 2

5. Training & Optimization
    o Loss: Logistic loss (binary cross-entropy)
    o Optimizer: COBYLA
    o Goal: Minimize classification loss
6. Evaluation
    Computes:
       o Train accuracy
       o Test accuracy
       o Predictions for sample inputs

## Installation

Install required dependencies:

pip install qiskit==2.0
pip install qiskit-aer
pip install pylatexenc
pip install scipy scikit-learn matplotlib

## How the Model Works

1. Encoding Classical Data
The encoder circuit:
- Rotates each qubit according to one feature
- Entangles qubits
- Adds a nonlinear term RZ(x0*x1)
- Produces a quantum state representing the sample

2. Variational Ansatz
- A 4-parameter variational layer controls how the model learns the classification boundary.

3. Prediction
- The PQC outputs an expectation value of the Pauli operator Z ⊗ I, which is mapped to a
probability.

4. Training
- The optimizer iteratively updates parameters θ to minimize prediction loss.

## Outputs
The script prints:
- Optimized parameters θ*
- Training accuracy
- Test accuracy
- Prediction details on sample test points

## Running the Project

Simply execute the script or notebook.
It will automatically:
1. Generate dataset
2. Build circuits
3. Train the model
4. Print metrics and predictions


