# Superconducting Quantum Research Program

## Chip Design Hackathon 2024

### Project 11. Transmon Energy Spectrum with QSM

This repository contains our Project 11 submission for the Chip Design
Hackathon 2024. The project demonstrates a complete workflow for
modeling a simplified transmon qubit using a truncated charge basis
Hamiltonian, computing its energy spectrum via diagonalization, and
studying how small Hermitian perturbations shift the spectrum. Alongside
the Hamiltonian model, we include a compact QSM example to verify basic
two qubit state preparation and state vector access.

------------------------------------------------------------------------

## Team

Tilock Sadhukhan (Team Leader)\
Indranil Ghosh\
Achyut Chebiyam\
Kazim Mumtaz\
Aniekan Afangideh

------------------------------------------------------------------------

## Demo Video Link

https://youtu.be/J3bacAgWORs?si=M1Ex9QVI--Wiy253

------------------------------------------------------------------------

## Physical Model

The starting point is the standard transmon Hamiltonian

$$
H = 4E_C \hat{n}^2 - E_J \cos(\hat{\phi})
$$

where $E_C$ is the charging energy, $E_J$ is the Josephson energy,
$\hat{n}$ is the charge number operator, and $\hat{\phi}$ is the
superconducting phase operator. Instead of working with the full
infinite dimensional Hilbert space, we truncate to a finite charge basis
and construct a matrix Hamiltonian suitable for numerical
diagonalization.

------------------------------------------------------------------------

## Truncated Charge Basis Approximation

We restrict charge states to

$$
n \in \Bigl\{-\frac{N}{2}, \ldots, \frac{N}{2}-1\Bigr\}
$$

The diagonal elements are

$$
H_{nn} = 4E_C n^2
$$

The cosine term introduces nearest neighbor coupling

$$
H_{n,n+1} = H_{n+1,n} = -\frac{E_J}{2}
$$

This yields a tridiagonal Hermitian matrix

$$
H =
\begin{pmatrix}
4E_C n_1^2 & -\frac{E_J}{2} & 0 & \cdots \\
-\frac{E_J}{2} & 4E_C n_2^2 & -\frac{E_J}{2} & \cdots \\
0 & -\frac{E_J}{2} & 4E_C n_3^2 & \cdots \\
\vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$

Since the matrix is Hermitian, its eigenvalues are real and correspond
to the energy levels of the truncated model.

------------------------------------------------------------------------

## Energy Spectrum

Energy levels are obtained by solving

$$
H|\psi_k\rangle = E_k|\psi_k\rangle
$$

Numerically computed using

``` python
eigenvalues, eigenvectors = np.linalg.eigh(H)
```

Plotting the eigenvalues gives the discrete energy spectrum.

------------------------------------------------------------------------

## Noise Model

To simulate imperfections, we add Gaussian random noise

$$
N_{ij} \sim \mathcal{N}(0,\sigma^2)
$$

and enforce Hermiticity

$$
H_{noisy} = H + \frac{N + N^T}{2}
$$

Diagonalizing $H_{noisy}$ reveals shifts in the energy levels.

------------------------------------------------------------------------

## QSM Verification Step

We initialize a two qubit system

$$
|\psi_0\rangle = |00\rangle
$$

Applying a Hadamard gate to qubit 0

$$
H|0\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)
$$

produces

$$
|\psi\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |10\rangle)
$$

This confirms correct state initialization and gate application within
QSM.

------------------------------------------------------------------------

## Running Locally

Create and activate a virtual environment.

Linux or macOS

``` bash
python3 -m venv .venv
source .venv/bin/activate
```

Windows PowerShell

``` powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Install dependencies

``` bash
pip install numpy matplotlib
```

If QSM is available

``` bash
pip install qsm
```

Run

``` bash
python transmon_simulation.py
```

You will see printed outputs and plots for both clean and noisy energy
spectra.

------------------------------------------------------------------------

## Scope and Notes

This is a simplified transmon model intended for educational and
exploratory purposes. The truncation dimension is small, and the noise
model is generic rather than hardware calibrated. Two transmon coupling
terms are not included in this version.

------------------------------------------------------------------------

## Keywords

Superconducting Qubits\
Transmon\
QSM\
Hamiltonian Simulation\
Energy Spectrum\
Noise Perturbation


