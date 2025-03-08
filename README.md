# Biological Balanced Networks Simulation

This project aims to study the asynchronous and irregular dynamics in cortical circuits using a balanced network model. The project builds a network composed of three neuronal populations—excitatory $E$, inhibitory $I$, and an external input $X$—to explore neuronal dynamics, input noise statistics, and the relationship between theoretical predictions and simulation results.

## Project Contents

The repository contains the following main files:

- **miniproject.ipynb**  
  A Jupyter Notebook containing code implementations and simulation results for generating Poisson spike trains, simulating a single LIF neuron with various input configurations, and running full network simulations.

- **mini-project.pdf**  
  A detailed project description that covers the network architecture, dynamical equations, time discretization methods, experimental tasks, and theoretical derivations. Topics include:
  - Generating 2-second-long independent Poisson spike trains with raster plots.
  - Simulating a single LIF neuron with a single input spike train.
  - Simulating a single LIF neuron with multiple inputs (both excitatory and inhibitory).
  - Assembling the full network and comparing simulation results with theoretical predictions.

## Model and Methods Overview

### Network Structure

- **Neuronal Populations**:  
  - **$E$ (Excitatory)**: Excitatory neurons.
  - **$I$ (Inhibitory)**: Inhibitory neurons.
  - **$X$ (External)**: External input neurons generating spikes via a Poisson process.

- **Connectivity**:  
  Each neuron in the $E$ and $I$ populations randomly receives inputs from $K$ neurons in each of the $E$, $I$, and $X$ populations. Synaptic weights are scaled by $\frac{J_{\alpha\beta}}{\sqrt{K}}$, where $J_{\alpha I} < 0$ (inhibitory) and $J_{\alpha E} > 0$, $J_{\alpha X} > 0$ (excitatory).

### Neuronal Dynamics

- **LIF Neuron Model**:  
  The membrane potential $V_i(t)$ of a neuron follows the differential equation:

  $$\frac{dV_i^\alpha(t)}{dt} = -\frac{V_i^\alpha(t)}{\tau} + \sum_{\beta \in \{E, I, X\}} \frac{J_{\alpha\beta}}{\sqrt{K}} \sum_{j \in C_i^{\alpha\beta}} S_j^\beta(t)$$

  When $V_i(t)$ exceeds the threshold $V_{th}$, the neuron emits a spike and its potential is reset.

- **Time Discretization**:  
  The continuous dynamics are discretized using the forward Euler method with a time step $\delta_t$. The discretized value at $t = k\delta_t$ is denoted by $\tilde{f}(k) = f(k\delta_t)$.

### Simulation Experiments

The project includes the following experiments:

1. **Generating Poisson Spike Trains**  
   - Generate independent Poisson spike trains over 2 seconds and create raster plots. Verify that the spike counts per neuron match theoretical expectations.

2. **Single LIF Neuron Simulation (Single Input)**  
   - Simulate a single LIF neuron receiving input from one Poisson neuron, and plot the membrane potential along with the input/output spike trains.

3. **Single LIF Neuron Simulation (Multiple Inputs)**  
   - Simulate a single LIF neuron receiving inputs from multiple Poisson neurons, analyze the mean and variance of the membrane potential, and compare with theoretical predictions.

4. **Simulation with Both Excitatory and Inhibitory Inputs**  
   - Investigate the response of a neuron receiving simultaneous excitatory and inhibitory inputs. Adjust parameters to achieve an output firing rate of about 10 Hz, and compute the Fano factor to evaluate spike count variability.

5. **Full Network Simulation**  
   - Assemble the full network with $E$, $I$, and $X$ populations by randomly generating connections. Simulate the network for different external input rates (e.g., $r_X$ at 5, 10, 15, and 20 Hz) and verify how the firing rates of the $E$ and $I$ populations vary according to theoretical predictions.

## Dependencies

- Python 3.x  
- Jupyter Notebook or Jupyter Lab  
- Common scientific libraries:  
  - NumPy  
  - Matplotlib  
  <!-- - (Optional) SciPy -->

It is recommended to create a virtual environment and install the dependencies using:

```bash
pip install numpy matplotlib jupyter
