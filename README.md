# Infection-Modelling-with-Ising-Lattice

# MCMC Ising Model for Disease Dynamics

This code implements a two-dimensional Ising-model simulation for modelling infectious-disease dynamics using a modified Monte Carlo approach.

The model maps Ising spin states onto epidemiological states:

- `-1` → healthy individual
- `+1` → infected individual

An additional `SIR_counter` tracks whether each lattice site is:

- **Susceptible (S)**
- **Infected (I)**
- **Recovered/immune (R)**

The model extends the standard Metropolis-Hastings Ising algorithm by introducing an **infectious time (`I_t`)** and **recovery/immunity time (`R_t`)**, allowing SIS, SIR and SIRS-like disease dynamics to be simulated.

## Main components

### `IsingModel`
Defines the 2D Ising lattice and provides methods for:

- initializing the lattice,
- calculating individual spin energies with periodic boundary conditions,
- flipping spins,
- calculating lattice magnetisation,
- tracking susceptible, infected and recovered states.

### `sweep_lattice()`
Performs one lattice sweep. Susceptible sites are considered in random order and infection events are accepted according to a Boltzmann-weighted transition probability.

### `simulate_MCMC()`
Runs the simulation for a specified number of lattice sweeps while tracking:

- magnetisation,
- energy,
- susceptible population,
- infected population,
- recovered population.

### `repeated_simulation()`
Repeats the MCMC simulation across multiple effective temperatures and independent sampling rounds to obtain statistically comparable results.

## Main parameters

- `M`, `N` – lattice dimensions
- `J` – nearest-neighbour interaction strength
- `H` – external field
- `kT` – effective temperature controlling stochasticity
- `n_sweeps` – number of lattice sweeps
- `n_burn_sweeps` – equilibration/burn-in period
- `I_t` – number of sweeps an individual remains infected
- `R_t` – number of sweeps an individual remains immune after recovery
- `n_repeat` – number of independent simulation repeats

## Requirements

The code is written in Python and uses:

```python
numpy
time
