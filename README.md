# Superconducting Quantum Research Program

## Chip Design Hackathon 2024

### Project 11 -- Transmon Modeling using QSM

------------------------------------------------------------------------

## Team Members

-   Tilock Sadhukhan (Team Leader)
-   Indranil Ghosh
-   Achyut Chebiyam
-   Kazim Mumtaz
-   Aniekan Afangideh

------------------------------------------------------------------------

# Project Overview

This project implements a simplified transmon qubit model using the
Qubit Simulation Module (QSM).

Goals:

-   Model a transmon Hamiltonian in a truncated charge basis
-   Compute its energy spectrum
-   Visualize eigenvalues
-   Study spectral shifts under Hermitian noise
-   Demonstrate basic QSM state preparation

------------------------------------------------------------------------

# Theoretical Background

## Transmon Hamiltonian

$$
H = 4E_C \hat{n}^2 - E_J \cos(\hat{\phi})
$$

Where:

-   $E_C$ = Charging energy\
-   $E_J$ = Josephson energy\
-   $\hat{n}$ = Charge operator\
-   $\hat{\phi}$ = Phase operator

------------------------------------------------------------------------

## Truncated Charge Basis Approximation

Charge states:

$$
n \in \left\{-\frac{N}{2}, \dots, \frac{N}{2}-1\right\}
$$

Diagonal terms:

$$
H_{nn} = 4E_C n^2
$$

Off-diagonal coupling:

$$
H_{n,n+1} = H_{n+1,n} = -\frac{E_J}{2}
$$

Matrix structure:

$$
H =
\begin{pmatrix}
4E_C n_1^2 & -\frac{E_J}{2} & 0 & \cdots \\
-\frac{E_J}{2} & 4E_C n_2^2 & -\frac{E_J}{2} & \cdots \\
0 & -\frac{E_J}{2} & 4E_C n_3^2 & \cdots \\
\vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$

------------------------------------------------------------------------

## Energy Spectrum

Solve the eigenvalue equation:

$$
H |\psi_k\rangle = E_k |\psi_k\rangle
$$

Computed using:

``` python
np.linalg.eigh(H)
```

------------------------------------------------------------------------

## Noise Model

Random Gaussian noise:

$$
N_{ij} \sim \mathcal{N}(0,\sigma^2)
$$

Hermitian perturbation:

$$
H_{noisy} = H + \frac{N + N^T}{2}
$$

------------------------------------------------------------------------

# QSM State Preparation

Initial state:

$$
|\psi_0\rangle = |00\rangle
$$

Apply Hadamard on qubit 0:

$$
H|0\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)
$$

Resulting state:

$$
|\psi\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |10\rangle)
$$

------------------------------------------------------------------------

# Installation

Create virtual environment:

Linux / macOS:

``` bash
python3 -m venv .venv
source .venv/bin/activate
```

Windows:

``` powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Install dependencies:

``` bash
pip install numpy matplotlib
```

If QSM is available:

``` bash
pip install qsm
```

------------------------------------------------------------------------

# Running the Simulation

``` bash
python transmon_simulation.py
```

You will see:

-   State vector output
-   Hamiltonian matrix
-   Eigenvalues
-   Energy spectrum plot
-   Noisy spectrum comparison

------------------------------------------------------------------------

# Code

``` python
from qsm import QSM
import numpy as np
import matplotlib.pyplot as plt

def initialize_qsm():
    num_qubits = 2
    qsm_system = QSM(num_qubits)
    return qsm_system

def define_transmon_hamiltonian(num_levels=4, E_C=0.2, E_J=1.0):
    n = np.arange(-num_levels // 2, num_levels // 2)
    H = np.diag(4 * E_C * (n**2))
    for i in range(len(n) - 1):
        H[i, i + 1] = H[i + 1, i] = -E_J / 2
    return H

def compute_energy_levels(H):
    eigenvalues, eigenvectors = np.linalg.eigh(H)
    return eigenvalues, eigenvectors

def plot_energy_spectrum(eigenvalues):
    plt.plot(eigenvalues, 'o')
    plt.xlabel('State Index')
    plt.ylabel('Energy Level')
    plt.title('Energy Spectrum')
    plt.grid(True)
    plt.show()

def add_noise_to_hamiltonian(H, noise_level=0.01):
    noise = noise_level * np.random.randn(*H.shape)
    return H + (noise + noise.T) / 2

if __name__ == "__main__":
    qsm_system = initialize_qsm()
    qsm_system.h(0)
    print("State Vector:", qsm_system.state_vector())

    H = define_transmon_hamiltonian()
    eigenvalues, _ = compute_energy_levels(H)
    plot_energy_spectrum(eigenvalues)

    noisy_H = add_noise_to_hamiltonian(H)
    noisy_eigenvalues, _ = compute_energy_levels(noisy_H)
    plot_energy_spectrum(noisy_eigenvalues)
```

------------------------------------------------------------------------

# Keywords

Superconducting Qubits\
Transmon\
QSM\
Hamiltonian Simulation\
Energy Spectrum\
Quantum Modeling

------------------------------------------------------------------------

Demo Video:\
https://youtu.be/J3bacAgWORs?si=M1Ex9QVI--Wiy253
