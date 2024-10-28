# Simple Quantum Network Simulation (SimpleQuantNetSim)

This repository provides a framework for simulating quantum entanglement distribution across complex mesh networks. The project models a network of quantum repeaters and implements various protocols to efficiently route multipartite entanglement. The repository includes scripts for setting up network graphs, executing entanglement distribution protocols, and analyzing repeater usage across different network topologies.

## Project Structure

- **`graph.py`**: Defines utility functions for managing quantum network graphs using the NetworkX library. This includes functions for entanglement-based subgraph extraction, dynamic node removal based on usage, and updating graph parameters based on entanglement status.

- **`graph_manager.py`**: Manages graph data input and output, including functions to save/load graphs in JSON format. Also includes tools for generating predefined graphs based on standard topologies (e.g., ARPAnet, NSFnet, UKnet).

- **`protocols.py`**: Implements various routing protocols for entanglement distribution:
  - **Shortest Path (SP)**: Distributes entanglement using the shortest available path.
  - **Multipath Greedy (MP-G)**: Generates entanglement along multiple paths, selecting the most promising for GHZ distribution.
  - **Multipath Cooperative (MP-C)**: Coordinates multiple paths to maximize entanglement rates while balancing resource usage.

- **`sim.py`**: Contains simulation functions, specifically managing the entanglement generation process, decoherence, and resource aging within the network. This includes `run_entanglement_step`, which simulates entanglement success based on edge probabilities.

- **`data`**: Stores graph data in JSON format, used for initializing specific topologies.

- **`figures`**: Outputs visualizations of network states and results from simulations, showing metrics like entanglement distribution rates and repeater usage.

- **`graphs`**: Contains the initial graph data in `.txt` format, describing the structure of various networks to be simulated.

## Key Concepts

### Quantum Repeaters and Entanglement Distribution
Quantum repeaters extend entanglement distribution across large networks by generating and managing entanglement links over shorter segments. This project focuses on simulating quantum repeater networks to test various entanglement routing protocols.

### Protocols
1. **SP Protocol**: A straightforward routing protocol that uses the shortest path for entanglement distribution. Efficient in simpler networks but less reliable in complex mesh topologies.
2. **MP-G Protocol**: Greedily selects paths to optimize entanglement success based on network state, balancing performance with computational complexity.
3. **MP-C Protocol**: A cooperative multipath protocol that coordinates across multiple paths, achieving high entanglement rates in dense networks at the expense of computational complexity.

### Simulation
The simulations assess repeater usage and entanglement distribution rates (DR), with results visualized in the `figures` folder. The impact of parameters such as perfect operations probability (`pop`) and decoherence parameter (`Qc`) is analyzed across various topologies.

## Getting Started

### Requirements
- Python 3.x
- NetworkX
- numpy

### Usage
1. **Graph Setup**: Initialize network topologies using `graph_manager.py`.
2. **Protocol Execution**: Run protocols via `protocols.py` to test entanglement distribution rates and repeater utilization.
3. **Simulation**: Execute simulations with `sim.py` to evaluate protocol performance and network resilience under varying conditions.

### Example
Run a sample simulation on the UKnet topology with the SP protocol:
```python
from simplequantnetsim import graph_manager, protocols, sim

# Load UKnet topology
G = graph_manager.load_graph("UKnet")

# Set up user nodes
users = ["node1", "node2", "node3"]

# Run SP protocol
er, generation_time, avg_links = protocols.SP_protocol(G, users, timesteps=500, reps=100)
