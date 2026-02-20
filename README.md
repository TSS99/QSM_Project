# QSM Project

Welcome to the team repository for the **Superconducting Quantum Research Program – Chip Design Hackathon 2024**.

---

## Team Members

- **Tilock Sadhukhan** (Team Leader)  
- Indranil Ghosh  
- Achyut Chebiyam  
- Kazim Mumtaz  
- Aniekan Afangideh  

---

## Project Overview

We implemented **Project 11**, which focuses on modeling two superconducting **transmon qubits** using the **Qubit Simulation Module (QSM)** and simulating their energy spectrum.

Our work combines quantum circuit simulation with a simplified Hamiltonian-based description of a transmon system.

---

## Theoretical Background

### Transmon Hamiltonian

A transmon qubit is described by the Hamiltonian:

\[
H = 4E_C \hat{n}^2 - E_J \cos(\hat{\phi})
\]

where:

- \( E_C \) → Charging energy  
- \( E_J \) → Josephson energy  
- \( \hat{n} \) → Charge operator  
- \( \hat{\phi} \) → Phase operator  

---

### Discretized Hamiltonian

In a truncated charge basis, the Hamiltonian is approximated as:

\[
H_{nn} = 4E_C n^2
\]

\[
H_{n,n+1} = H_{n+1,n} = -\frac{E_J}{2}
\]

This results in a matrix of the form:

\[
H =
\begin{pmatrix}
4E_C n_1^2 & -\frac{E_J}{2} & 0 & \cdots \\
-\frac{E_J}{2} & 4E_C n_2^2 & -\frac{E_J}{2} & \cdots \\
0 & -\frac{E_J}{2} & 4E_C n_3^2 & \cdots \\
\vdots & \vdots & \vdots & \ddots
\end{pmatrix}
\]

---

### Energy Spectrum

The energy levels are obtained by solving the eigenvalue problem:

\[
H |\psi_k\rangle = E_k |\psi_k\rangle
\]

where:

- \( E_k \) → Energy eigenvalues  
- \( |\psi_k\rangle \) → Eigenstates  

---

### Noise Model

To simulate experimental imperfections, random Hermitian noise is added:

\[
H_{\text{noisy}} = H + \frac{N + N^T}{2}
\]

where:

\[
N_{ij} \sim \mathcal{N}(0, \sigma^2)
\]

This preserves Hermiticity while introducing perturbations.

---

## Simulation Workflow

### 1. QSM Initialization

We initialize a two-qubit quantum system:

\[
|\psi_0\rangle = |00\rangle
\]

---

### 2. State Preparation

A Hadamard gate is applied to qubit 0:

\[
H |0\rangle =
\frac{1}{\sqrt{2}} (|0\rangle + |1\rangle)
\]

Resulting state:

\[
|\psi\rangle =
\frac{1}{\sqrt{2}} (|00\rangle + |10\rangle)
\]

---

### 3. Hamiltonian Construction

We construct a truncated transmon Hamiltonian:

\[
H = 4E_C n^2 - \frac{E_J}{2} (|n\rangle\langle n+1| + |n+1\rangle\langle n|)
\]

---

### 4. Diagonalization

Energy levels are computed via:

\[
E_k = \text{eig}(H)
\]

---

### 5. Visualization

We plot:

- Discrete quantum states  
- Corresponding energy eigenvalues  

---

## Results

The simulation produced:

- A discrete energy spectrum  
- Clear separation of eigenstates  
- Observable shifts under noise perturbation  

This provides insight into the behavior of a simplified transmon system.

---


Key components:

- Hamiltonian definition  
- Eigenvalue computation  
- Noise modeling  
- Energy spectrum visualization  

---

## Project Demonstration

A detailed explanation of the project is available here:

📺 **YouTube Video**  
https://youtu.be/J3bacAgWORs?si=M1Ex9QVI--Wiy253

---

## Keywords

Superconducting Qubits • Transmon • QSM • Hamiltonian Simulation • Energy Spectrum • Quantum Modeling
