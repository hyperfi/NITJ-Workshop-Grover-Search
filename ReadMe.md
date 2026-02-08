# Grover's Search Algorithm - NITJ Workshop

A comprehensive hands-on workshop exploring **Grover's quantum search algorithm** with practical exercises using Qiskit. This repository contains implementations and experiments demonstrating key concepts of quantum computing and quantum search.

## Overview

Grover's Algorithm is one of the most important quantum algorithms, providing a **quadratic speedup** for unstructured database search. This workshop provides both theoretical understanding and practical implementation experience using IBM's Qiskit framework.

### Key Concepts Covered
- **Quantum Oracles**: Marking target states in quantum superposition
- **Diffusion Operator**: Amplifying marked states while suppressing unmarked ones
- **Amplitude Amplification**: The core mechanism of Grover's algorithm
- **Quantum Speedup**: How quantum search scales differently than classical search
- **Algorithm Periodicity**: Understanding over-rotation and optimal iteration counts

## Repository Structure

```
NITJ-Workshop-Grover-Search/
├── ReadMe.md                          # This file
├── Helper_Functions.py                # Reusable quantum functions
├── Grover_Lab_experiment_1.ipynb      # Exercise 1: Scaling with qubits
├── Grover_Lab_experiment_2.ipynb      # Exercise 2: Over-rotation phenomenon
└── Grover_Lab_experiment_3.ipynb      # Exercise 3: Multiple solutions & efficiency
```

## Files Description

### Helper_Functions.py
Provides three core functions for implementing Grover's algorithm:

- **`Grover_oracle(marked_states)`**
  - Creates a quantum oracle that marks target states with a phase flip
  - Supports multiple marked states
  - Returns a `QuantumCircuit` implementing the oracle
  
- **`Grover_operator(oracle, insert_barriers, name)`**
  - Constructs the full Grover iteration operator (oracle + diffusion)
  - Includes controlled Hadamard gates and multi-controlled NOT gates
  - Optional barrier visualization for circuit inspection

- **`Get_Data_from_Fake_backend(shots, circuit, fake_backend)`**
  - Transpiles and runs circuits on simulated backends
  - Returns measurement statistics without requiring actual hardware
  - Uses Qiskit Runtime Sampler for efficient execution

### Experiment Notebooks

#### **Exercise 1: Searching a Larger Space** (`Grover_Lab_experiment_1.ipynb`)
**Objective**: Understand algorithm scaling with search space size

**Tasks**:
1. Search for single states in 4-qubit and 5-qubit systems
2. Calculate optimal iterations: `N_opt = ⌊π/4 × arcsin(√(M/N))⌋`
   - Where M = number of marked states, N = 2^n total states
3. Observe how iteration count grows with qubit count

**Key Insight**: For small marked state fractions, optimal iterations ~π/4 × √N

---

#### **Exercise 2: The Phenomenon of Over-Rotation** (`Grover_Lab_experiment_2.ipynb`)
**Objective**: Demonstrate algorithm periodicity and the dangers of over-iteration

**Tasks**:
1. Use marked states: `["0110", "1001"]` in 4-qubit system
2. Run with optimal iterations (2) vs. forced iterations (5)
3. Compare success probability histograms

**Key Insight**: Grover's algorithm exhibits sinusoidal behavior. Running too many iterations decreases success probability—finding the optimal count is critical.

---

#### **Exercise 3: Multiple Solutions and Efficiency** (`Grover_Lab_experiment_3.ipynb`)
**Objective**: Explore how solution density affects search efficiency

**Tasks**:
1. Define multiple marked states (e.g., 4 from 16 possibilities)
2. Calculate optimal iterations with M/N = 0.25
3. Analyze success rates and iteration efficiency

**Key Insight**: Higher solution density requires fewer iterations, but the relationship is non-linear and sinusoidal.

## Prerequisites & Installation

### Required Libraries
```bash
pip install qiskit==2.3.0 qiskit-ibm-runtime qiskit-aer numpy matplotlib
```

### Python Version
- **Python 3.13.5** (required)

### Dependencies
- **Qiskit**: Quantum computing framework
- **Qiskit IBM Runtime**: For running on simulators and real backends
- **NumPy**: Numerical computations
- **Matplotlib**: Visualization (used for circuit and histogram plots)

## How to Run

### Option 1: Using Jupyter Notebook/Lab
```bash
jupyter notebook Grover_Lab_experiment_1.ipynb
```

### Option 2: Using VS Code
1. Install the Jupyter extension in VS Code
2. Open any `.ipynb` file
3. Run cells sequentially or use "Run All"

## Mathematical Background

### Grover Algorithm Steps
1. **Initialize**: Create equal superposition of all basis states
   ```
   |ψ⟩ = H⊗n |0⟩⟨n⟩ = 1/√N ∑ |x⟩
   ```

2. **Apply Oracle**: Phase-flip marked states
   ```
   O_f |x⟩ = (-1)^f(x) |x⟩
   ```

3. **Apply Diffusion**: Amplify marked state amplitudes
   ```
   D = 2|ψ⟩⟨ψ| - I
   ```

4. **Repeat**: Apply (Oracle + Diffusion) ≈ π/4 × √N times

5. **Measure**: Measure in computational basis

### Complexity
- **Classical**: O(N) in worst case
- **Quantum (Grover)**: O(√N) 
- **Speedup**: Quadratic improvement

## Expected Outcomes

### Exercise 1: Scaling Behavior
- 3-qubit (N=8, M=1): ~2 iterations
- 4-qubit (N=16, M=1): ~2 iterations  
- 5-qubit (N=32, M=1): ~3 iterations

### Exercise 2: Over-Rotation Effects
- Optimal (2 iterations): ~90%+ success rate
- Over-rotated (5 iterations): 30-50% success rate (degraded performance)

### Exercise 3: Multiple Solutions
- M/N = 0.25: Often optimal at 1 iteration
- Higher solution density = faster convergence

## References & Further Reading

### Quantum Computing Fundamentals
- [Qiskit Textbook - Grover's Algorithm](https://qiskit.org/learn/course/foundations-course)
- Nielsen & Chuang: "Quantum Computation and Quantum Information"

### Qiskit Documentation
- [Qiskit Runtime Sampler](https://quantum.cloud.ibm.com/docs/en/api/qiskit-ibm-runtime/sampler-v2)
- [Circuit Library](https://quantum.cloud.ibm.com/docs/en/api/qiskit/circuit)



## Troubleshooting

### Import Errors
```python
# Ensure all dependencies are installed
pip install --upgrade qiskit qiskit-ibm-runtime qiskit-aer
```

### Kernel Issues in Jupyter
- Restart kernel before running cells
- Clear outputs and re-run sequentially

## Contributors

**NITJ Workshop Series** - Quantum Computing Lab

## License

See LICENSE file for details.

---

**Happy Quantum Computing! 🎉**

For questions or suggestions, please refer to the original workshop materials or Qiskit documentation.