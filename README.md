# Qiskit Fall Fest 2026 — Challenge Solutions

![IBM Quantum](https://img.shields.io/badge/IBM%20Quantum-Qiskit%202.x-0062FF?style=for-the-badge&logo=ibm)
![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python)
![Miniconda](https://img.shields.io/badge/Miniconda-Jupyter-3EB049?style=for-the-badge&logo=anaconda)

Complete solutions and Jupyter Notebook implementations for all four challenges of **Qiskit Fall Fest 2026** hosted by **Vishnu Institute of Technology** in collaboration with **IBM Quantum**.

---

## 📚 Overview of Challenges

| Challenge | Topic | Objective | Key Quantum Concepts |
| :--- | :--- | :--- | :--- |
| **[Challenge 1](Challenge_1_Predict_the_Output.ipynb)** | Predict the Output | Predict and compare measurement outcomes of single-qubit circuits | Pauli-$X$ (NOT), Hadamard ($H$), Basis states, Superposition, Deterministic vs Probabilistic |
| **[Challenge 2](Challenge_2_Make_the_Quantum_Coin_Biased.ipynb)** | Make the Quantum Coin Biased | Modify a single-qubit circuit to control measurement probabilities | $R_y(\theta)$ rotation, Bloch sphere geometry, Phase interference ($H-P-H$), Born's Rule |
| **[Challenge 3](Challenge_3_Can_you_change_the_correlation.ipynb)** | Can You Change the Correlation? | Modify a Bell state with $\le 1$ gate to change two-qubit correlation | Bell State $|\Phi^+\rangle$, Entanglement, Anti-correlation, CNOT, State $|\Psi^+\rangle$ |
| **[Challenge 4](Challenge_4_Quantum_Correlation_Switch.ipynb)** | Quantum Correlation Switch | Design a circuit switch between correlated (`00`, `11`) and opposite (`01`, `10`) | Correlation switching, Symmetric vs Anti-symmetric Bell pairs, Measurement statistics |

---

## 🔬 Detailed Challenge Summaries

### 1. Challenge 1: Predict the Output
- **Circuit A (Single $X$ gate)**:
  - Initial state: $|0\rangle \xrightarrow{X} |1\rangle$
  - Prediction: 100% outcome `1` (100 counts in 100 shots).
  - Actual: `{'1': 100}` (Matches prediction).
- **Circuit B (Two $X$ gates)**:
  - Initial state: $|0\rangle \xrightarrow{X} |1\rangle \xrightarrow{X} |0\rangle$ (since $X^2 = I$).
  - Prediction: 100% outcome `0` (100 counts in 100 shots).
  - Actual: `{'0': 100}` (Matches prediction).
- **Circuit C (Single $H$ gate)**:
  - Initial state: $|0\rangle \xrightarrow{H} \frac{|0\rangle + |1\rangle}{\sqrt{2}}$
  - Prediction: Superposition with $P(0) = 50\%$, $P(1) = 50\%$.
  - Actual: Approximately 50/50 distribution. Does not produce the exact same outcome on every shot due to probabilistic wavefunction collapse.

---

### 2. Challenge 2: Make the Quantum Coin Biased
- **Biasing Mechanism**:
  A standard Hadamard creates a fair quantum coin ($P(0) = P(1) = 0.5$).
  By using rotation gate $R_y(\theta)$, the state is:
  $$|\psi\rangle = R_y(\theta)|0\rangle = \cos\left(\frac{\theta}{2}\right)|0\rangle + \sin\left(\frac{\theta}{2}\right)|1\rangle$$
  - **Circuit 1 (Biased towards 0)**: Set $\theta = \frac{\pi}{3} \implies P(0) = \cos^2(\pi/6) = 75\%$, $P(1) = 25\%$.
  - **Circuit 2 (Biased towards 1)**: Set $\theta = \frac{2\pi}{3} \implies P(0) = 25\%$, $P(1) = \sin^2(\pi/3) = 75\%$.
  - **Interferometric Bias**: Also implemented via quantum interference using $H - P(\phi) - H$.
- **Challenge Question Answer**:
  *How can quantum gates change the probability of obtaining 0 or 1 when a qubit is measured?*
  Quantum gates perform unitary transformations that rotate the qubit's state vector $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$ on the Bloch sphere. According to Born's Rule, the measurement probability in the computational basis is determined by the squared magnitudes of the probability amplitudes ($P(0)=|\alpha|^2$, $P(1)=|\beta|^2$). Continuous rotation gates (e.g. $R_y(\theta)$) or interference paths ($H-P(\phi)-H$) tune the polar angle $\theta$, redistributing the probability amplitudes away from equal superposition to achieve any chosen degree of bias.

---

### 3. Challenge 3: Can You Change the Correlation?
- **Original Circuit**: Bell state $|\Phi^+\rangle = \frac{|00\rangle + |11\rangle}{\sqrt{2}}$ using $H(0)$ and $CX(0, 1)$.
  - Outcomes: Strongly correlated (`00` and `11` at ~50% each; `01` and `10` at 0%).
- **Modified Circuit**: Added **1 gate** ($X$ gate on qubit 1 after CNOT):
  $$|\Phi^+\rangle \xrightarrow{X_1} |\Psi^+\rangle = \frac{|01\rangle + |10\rangle}{\sqrt{2}}$$
- **Result**: Perfectly transformed the relationship from positive correlation (`00`, `11`) into anti-correlation (`01`, `10`).

---

### 4. Challenge 4: Quantum Correlation Switch
- **Part A (Correlated Outcomes)**:
  - State: $|\Phi^+\rangle = \frac{|00\rangle + |11\rangle}{\sqrt{2}}$
  - Measured Outcomes: Exclusively `00` and `11` (100 shots).
- **Part B (Opposite Outcomes)**:
  - State: $|\Psi^+\rangle = \frac{|01\rangle + |10\rangle}{\sqrt{2}}$ by toggling the switch ($X$ on qubit 1).
  - Measured Outcomes: Exclusively `01` and `10` (100 shots).
- **Part C (Comparison & Physical Mechanism)**:
  - Entanglement binds qubit 0 to qubit 1. The bit-flip gate $X$ maps $|00\rangle \mapsto |01\rangle$ and $|11\rangle \mapsto |10\rangle$, switching the joint measurement statistics from identical to opposite.

---

## 📁 Repository Structure

```text
├── Challenge_1_Predict_the_Output.ipynb         # Challenge 1 notebook (Executed with outputs)
├── Challenge_2_Make_the_Quantum_Coin_Biased.ipynb     # Challenge 2 notebook (Executed with outputs)
├── Challenge_3_Can_you_change_the_correlation.ipynb   # Challenge 3 notebook (Executed with outputs)
├── Challenge_4_Quantum_Correlation_Switch.ipynb       # Challenge 4 notebook (Executed with outputs)
├── Qiskit_Fall_Fest_2026_All_Challenges.ipynb         # Master notebook containing all 4 solutions
├── challenge 1.pdf                                    # Problem statement 1
├── challenge 2.pdf                                    # Problem statement 2
├── challenge 3.pdf                                    # Problem statement 3
├── challenge 4.pdf                                    # Problem statement 4
└── README.md                                          # Documentation and analysis
```

---

## 🚀 Running the Notebooks in Miniconda

1. **Activate your conda environment**:
   ```bash
   conda activate qiskit-fallfest
   ```

2. **Launch Jupyter Notebook or JupyterLab**:
   ```bash
   jupyter notebook
   # or
   jupyter lab
   ```

3. **Dependencies**:
   ```bash
   pip install "qiskit>=2.0.0" qiskit-aer matplotlib pylatexenc
   ```

---

## 👩‍💻 Author
- **GitHub**: [@patan-shehanaz](https://github.com/patan-shehanaz)
- **Institution**: Vishnu Institute of Technology
- **Event**: Qiskit Fall Fest 2026 (IBM Quantum)
