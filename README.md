<!-- # JaxADi -->
<!-- TODO: ADD PATCHES -->

<p align="center">
  <!-- Placeholder for a cool logo -->
  <img src="https://github.com/based-robotics/jaxadi/blob/master/_assets/_logo.png?raw=true" alt="JAXADI Logo" width="400"/>
</p>


**JaxADi** is a powerful Python library designed to bridge the gap between `casadi.Function` and JAX-compatible functions. By leveraging the strengths of both CasADi and JAX, JAXADI opens up exciting opportunities for building highly efficient, batchable code that can be executed seamlessly across CPUs, GPUs, and TPUs.

JAXADI can be particularly useful in scenarios involving:

- Robotics simulations
- Optimal control problems
- Machine learning models with complex dynamics
- Large-scale numerical optimizations


## Installation

You can install JAXADI using pip:
<!-- Change once it will be realeased -->

```bash
pip install jaxadi
```

For a complete environment setup, we recommend using Conda/Mamba:

```bash
mamba env create -f environment.yml
```

## Usage

JAXADI provides a simple and intuitive API:

```python
import casadi as cs
import numpy as np
from jaxadi import translate, convert
from jax import numpy as jnp

x = cs.SX.sym("x", 2, 2)
y = cs.SX.sym("y", 2, 2)
# Define a complex nonlinear function
z = x @ y  # Matrix multiplication
z_squared = z * z  # Element-wise squaring
z_sin = cs.sin(z)  # Element-wise sine
result = z_squared + z_sin  # Element-wise addition
# Create the CasADi function
casadi_fn = cs.Function("complex_nonlinear_func", [x, y], [result])
# Get JAX-compatible function string representation
jax_fn_string = translate(casadi_fn)
print(jax_fn_string)
# Define JAX function from CasADi one
jax_fn = convert(casadi_fn, compile=True)
# Run compiled function
input_x = jnp.array(np.random.rand(2, 2))
input_y = jnp.array(np.random.rand(2, 2))
output = jax_fn(input_x, input_y)

```

## Examples

JAXADI comes with several examples to help you get started:

1. [Basic Translation](examples/00_translate.py): Learn how to translate CasADi functions to JAX. 

2. [Lowering Operations](examples/01_lower.py): Understand the lowering process in JaxADi. 

3. [Function Conversion](examples/02_convert.py): See how to fully convert CasADi functions to JAX. 

4. [Pinocchio Integration](examples/03_pinocchio.py): Explore how to convert Pinocchio-based CasADi functions to JAX. 


> **Note**: To run the Pinocchio example, ensure you have Pinocchio properly installed in your environment.


## Performance Benchmarks

(Consider adding a section about performance comparisons between CasADi and JAXADI-translated functions)

<!-- ## Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for more details. -->

## Acknowledgements

This project draws inspiration from [cusadi](https://github.com/se-hwan/cusadi), with a focus on simplicity and JAX integration.

## Contact

For questions, issues, or suggestions, please [open an issue](https://github.com/based-robotics/jaxadi/issues) on our GitHub repository.


We hope JAXADI empowers your numerical computing and optimization tasks! Happy coding!
