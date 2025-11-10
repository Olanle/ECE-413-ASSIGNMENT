# ECE-413-ASSIGNMENT

-----

# ⛓️ Markov Chain Python Module

This repository contains a set of Python functions that define, validate, simulate, and analyze a simple **cyclic Markov Chain**. The module compares the theoretical long-term behavior (stationary distribution) with the results from a practical simulation.

-----

## 🧐 Conceptual Overview

A **Markov Chain** is a system that transitions between states based on probabilities. Its defining feature is the **Markov Property**: the probability of the next state depends **only** on the **current state**, not on the sequence of events that led up to it.

The primary goal of this module is to demonstrate that, over a long period, the time spent in each state during a simulation (the **Empirical Distribution**) converges to the mathematically predicted stable distribution (the **Stationary Distribution**).

-----

## ⚙️ Module Components

The module is structured around four core functions and a main test driver. It requires the `numpy` and `math` libraries.

### 1\. The Transition Matrix ($P$)

| Function | Role |
| :--- | :--- |
| `create_transition_matrix(N, self_prob, next_prob)` | Creates the $N \times N$ matrix $P$. This matrix holds the transition probabilities. In this specific implementation, each state has a `self_prob` chance of staying and a `next_prob` chance of moving to the next state cyclically. |
| `validate_matrix(P)` | Checks that the matrix $P$ is **row-stochastic**, meaning every row's probabilities must sum exactly to **1.0**. This is a fundamental requirement for a valid probability matrix. |

### 2\. Stationary Distribution (Theoretical)

| Function | Role |
| :--- | :--- |
| `compute_stationary_distribution(P, tol, max_iter)` | Calculates the long-term stable probability distribution, $\pi$. This is the theoretical probability of finding the system in any given state after an infinite number of steps. It is found by solving the equation $\mathbf{\pi P = \pi}$ using the **Power Method** (repeated matrix-vector multiplication). |

### 3\. Simulation (Empirical)

| Function | Role |
| :--- | :--- |
| `simulate_markov_chain(P, steps, initial_state)` | Runs a practical simulation of the chain for a specified number of `steps`. It uses `numpy.random.choice` to randomly select the next state based on the current state's transition probabilities. The output is the **Empirical Distribution**—the fraction of total steps spent in each state. |

### 4\. Testing and Entropy

| Function | Role |
| :--- | :--- |
| `test_markov_module(N, steps)` | The main function that orchestrates the entire process: creates $P$, computes $\pi_{\text{theoretical}}$, runs the simulation to get $\pi_{\text{empirical}}$, and prints a detailed comparison of the two distributions. |
| `entropy(p, base)` | A standalone utility to measure the **uncertainty** or **randomness** of a probability distribution (like $\pi$). A uniform distribution (all states equally likely) has the maximum possible entropy. |

-----

## 🚀 How to Run the Module

The entire module can be executed via the `if __name__ == "__main__":` block at the end of the script.

### Example Execution

The main function runs the full test and comparison:

```python
if __name__ == "__main__":
    # Run a test with 5 states (N=5) and 100,000 steps
    test_markov_module(N=5, steps=100000)
```

### Expected Output Insight

Since the `create_transition_matrix` function builds a perfectly symmetrical (cyclic) chain, the theoretical stationary distribution ($\pi$) should be **uniform**.

$$\pi_{\text{theoretical}} = [0.2, 0.2, 0.2, 0.2, 0.2]$$

The output will demonstrate that the **Empirical Distribution** from the 100,000-step simulation closely matches this theoretical uniform distribution, confirming the correctness of both the theoretical computation and the simulation model.
