# Logical Factorisation Machines

Requires Python 3 and the [numba](numba.pydata.org) package.
The easiest way is to use the [Anaconda Python distribution](https://www.anaconda.com/download).
See [here](https://pypi.python.org/pypi/numba) numba installation instructions.

For installation got to the cloned directory and do `pip install .`.

## Basic usage example

```
import lom

# generate toy data
N = 10
D = 5
L = 3
Z = np.array(np.random.rand(N,L) > .5, dtype=np.int8)
U = np.array(np.random.rand(D,L) > .5, dtype=np.int8)
X = aux.lom_generate_data([2 * Z-1, 2 * U-1], model='OR-AND')

# initialise model
orm = lom.Machine()
data = orm.add_matrix(X, fixed=True)
layer = orm.add_layer(latent_size=3, child=data, model='OR-AND')

# initialise factors (optional)
layer.factors[0].val = np.array( 2*(np.random.rand(N, L) > .5) - 1, dtype=np.int8)

# run inference
orm.infer(burn_in_min=100, burn_in_max=1000, fix_lbda_iters=10, no_samples=50)

# to inspect results do 
# [layer.factors[i].show() for i in range(len(factors))]
```