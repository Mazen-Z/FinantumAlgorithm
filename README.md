# VQE Portfolio Optimization Algorithm

A quantum algorithm based on the Variational Quantum Eigensolver (VQE) for optimizing a stock portfolio. The algorithm can be customized to leverage quantum computing such as AWS Braket, Nvidia CUDA-Q, IonQ, Rigetti Quil, IBM Q, etc. and is implemented in a Qiskit powered, qBraid notebook environment.

## Table of Contents
- [Introduction](#introduction)
- [Algorithm Overview](#algorithm-overview)
- [Setup](#setup)
  - [Prerequisites](#prerequisites)
- [Outputs](#outputs)
  - [Portfolio Selection](#portfolio-selection)
- [Customization](#customization)

---

## Introduction

The **VQE Portfolio Optimization Algorithm** uses the **Variational Quantum Eigensolver (VQE)** to solve a portfolio optimization problem in the context of stock investments. It leverages quantum resources provided by **AWS Braket** and is run within a **qBraid notebook** environment. The goal of the algorithm is to select an optimal portfolio of stocks that balances risk and return.

This implementation is designed to:
- Select an optimal portfolio of stocks.
- Allocate a portion of a defined budget to each stock.
- Provide human-readable outputs for stock inclusion and monetary allocations.

## Algorithm Overview

### Variational Quantum Eigensolver (VQE)
The VQE is a hybrid quantum-classical algorithm used to find the minimum eigenvalue of a Hamiltonian. In this context, the Hamiltonian represents the risk-return tradeoff in a portfolio optimization problem.

The VQE involves:
- **Ansatz**: A parameterized quantum circuit (here, `TwoLocal`).
- **Optimizer**: A classical optimizer (here, `COBYLA`), which adjusts the circuit parameters to minimize the expectation value of the Hamiltonian.

### Portfolio Optimization
The portfolio optimization problem is formulated with:
- A set of stocks, represented by their historical returns and covariance matrix.
- A risk aversion parameter, which adjusts the balance between risk and return.
- A budget, which defines the total amount of money available for allocation across stocks.

## Setup

### Prerequisites
To run this algorithm, you will need:
- An account with **AWS Braket** for quantum computing resources.
- **qBraid Lab** setup for development.
- Python environment with necessary libraries installed.

## Outputs

The algorithm provides two key outputs: **Portfolio Selection** and **Budget Allocation**. These results help in deciding which stocks to include in the portfolio and how much of the available budget should be allocated to each stock.

### Portfolio Selection

The **Portfolio Selection** step determines which stocks from the provided dataset should be included in the optimized portfolio. This decision is based on the results of the quantum VQE algorithm. 

1. **Aggregated Parameters**: Each stock is represented by quantum rotation parameters. These parameters are aggregated (averaged) to determine whether the stock should be included in the portfolio.
   
2. **Thresholding**: A threshold is applied to the aggregated parameters. If the absolute value of the aggregated parameter for a stock exceeds the threshold, the stock is **included** in the portfolio. If not, it is **excluded**.

3. **Output**: For each stock, a decision is printed (either **Include** or **Do not include**) along with the aggregated quantum rotation value used to make the decision.

#### Example Output:
```plaintext

Optimal Portfolio Selection:
Stock AAPL: Include (Aggregated Rotation = 2.6864)
Stock AMZN: Do not include (Aggregated Rotation = 1.4502)
Stock GOOGL: Do not include (Aggregated Rotation = 0.9208)
Stock FB: Include (Aggregated Rotation = 2.3328)
Stock NVDA: Include (Aggregated Rotation = 3.8687)
Stock ADBE: Include (Aggregated Rotation = 2.9339)
Stock MSFT: Do not include (Aggregated Rotation = 0.6665)
Stock AMD: Include (Aggregated Rotation = 1.7071)
Stock INTC: Include (Aggregated Rotation = 2.6567)
Stock TSLA: Do not include (Aggregated Rotation = 1.3680)
Stock IBM: Include (Aggregated Rotation = 2.8334)
Stock ORCL: Do not include (Aggregated Rotation = 0.0046)
Stock JPM: Do not include (Aggregated Rotation = 0.1848)
Stock CRM: Include (Aggregated Rotation = 1.6933)
Stock MS: Include (Aggregated Rotation = 3.9054)
Stock NOW: Do not include (Aggregated Rotation = 1.5700)
Stock PLTR: Do not include (Aggregated Rotation = 1.0470)
Stock LMT: Do not include (Aggregated Rotation = 1.4960)
Stock DIS: Include (Aggregated Rotation = 3.7771)
Stock WFC: Include (Aggregated Rotation = 1.6663)

Selected Assets for Optimal Portfolio and Budget Allocations:
AAPL: 6.93% of budget, $6929.31
FB: 6.02% of budget, $6017.10
NVDA: 9.98% of budget, $9978.83
ADBE: 7.57% of budget, $7567.69
AMD: 4.40% of budget, $4403.25
INTC: 6.85% of budget, $6852.70
IBM: 7.31% of budget, $7308.38
CRM: 4.37% of budget, $4367.70
MS: 10.07% of budget, $10073.47
DIS: 9.74% of budget, $9742.66
WFC: 4.30% of budget, $4297.96

```
## Customization

The user is able to:
1. select the investment budget for the portfolio 
2. select what stock csv files to load
3. select the asset names
4. select the threshold of risk
5. selet the number of iterations to run when creating a suggested investment portfolio



