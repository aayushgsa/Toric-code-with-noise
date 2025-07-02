# Toric Code with Noise Simulation

This repository contains a Python notebook for simulating the performance of the toric code, a cornerstone of quantum error correction. The simulation explores the code's resilience to errors under two different physical models: one with perfect error detection and a more realistic one that includes measurement errors.
The primary goal is to visualize the threshold behavior of the toric code, demonstrating how increasing the code size (L) improves the logical qubit's robustness against physical errors. The simulations are built using NumPy, SciPy, and the PyMatching library for efficient Minimum-Weight Perfect Matching (MWPM) decoding.

## How It Works

The simulation is divided into two main stages, each exploring a different noise model.

Stage 1: Ideal Syndrome Simulation

In this stage, we simulate bit-flip and phase-flip errors occurring on the physical data qubits. However, we assume that the process of measuring the error syndromes (i.e., checking which stabilizers are violated) is perfect. The decoder is given a flawless snapshot of the errors' effects and must find the most likely error chain that produced it. This serves as a baseline for the code's performance under ideal conditions.

Stage 2: Noisy Syndrome Simulation

This is a more physically realistic model. In addition to the data qubit errors from Stage 1 (at rate p), the syndrome measurements themselves can be faulty (at rate q). An incorrect measurement can hide a real error or falsely report one, confusing the decoder.
To handle this, the simulation introduces a time-like dimension. We perform multiple rounds of syndrome measurements, creating a 3D space-time graph of detection events. The MWPM decoder then finds the most likely error chains not just in space, but across time, allowing it to distinguish between a data qubit error and a transient measurement error. This method is based on the work of Dennis, Kitaev, Landahl, and Preskill in arXiv:quant-ph/0110143.

## Key Features

Toric Code Construction: Procedurally generates the stabilizer check matrices and logical operators for a toric code of any given size L.
Two Noise Models:
Ideal bit/phase errors with perfect syndrome measurement.
Realistic errors with noisy syndrome measurements.
MWPM Decoding: Utilizes the efficient pymatching library for decoding.
Space-Time Decoding: Implements decoding over a 3D matching graph to handle measurement errors.
Performance Visualization: Plots the logical error rate against the physical error rate to show the code's error correction threshold.

## Run the simulations:
You can run the cells sequentially. The notebook is divided into the two stages described above. Each stage has its own parameters (shots, L values, error rates p) that you can modify at the top of the cell before running.
Stage 1 Cell: Runs the simulation with ideal syndromes and plots the results.
Stage 2 Cell: Runs the more intensive simulation with noisy syndromes and plots the results on a log scale.
After running a simulation cell, a plot will be generated showing the logical error rate as a function of the physical error rate for different code sizes. This visualization is key to seeing the error-correcting power of the toric code in action.
