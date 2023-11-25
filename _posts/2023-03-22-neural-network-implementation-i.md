---
layout: post
title: Neural Network Implementation I
date: 2023-03-22 09:36:00
tags: [Artificial Intelligence, Data Science, Machine Learning, Neural Networks, Python, Statistics]
---
## Neural Network Implementation I

**(This article is a work-in-progress).**

With fundamentals from past posts on the architecture of **neural networks**, evaluating predictive models, and a look into various activation functions, we can now bring all the elements together.

I'll be detailing a simple implementation of a single layer neural network in Python to toy around with.

<!--
![Deep Learning Neural Network](/docs/assets/images/dl.png)

**Figure 1.** *Deep Learning Neural Network with Multiple Layers*
-->

### Libraries

```python
import numpy as np
from typing import Callable, List, Dict, Tuple
```

### Computing Root Mean Squared Error (RMSE)<sup>[[1]](https://sajidsarker.github.io/2023/02/09/evaluating-predictive-models.html)</sup>
```python
def compute_rmse(predictions: np.ndarray, actuals: np.ndarray) -> float:
    return np.sqrt(np.mean(np.power(predictions-actuals, 2)))
```

### Activation Function<sup>[[2]](https://sajidsarker.github.io/2023/02/27/activation-functions.html)</sup>
```python
def sigmoid(x: np.ndarray) -> np.ndarray:
    return 1 / (1 + np.exp(-x))
```

### Random Initialisation

In a neural network, the initial weights for each layer of perceptrons must be randomised to values in the $$\epsilon$$-neighbourhood of 0, for a real $$\epsilon$$ that is very small.

Initialising initial weights to 0 causes the model to be stuck, as the forward pass will continue to evaluate to 0, gleaning no further information during backwards propagation for model weight updates. 

```python
def initialise_weights(num_features: int) -> Dict[str, np.ndarray]:
    weights: Dict[str, np.ndarray] = {}

    weights['Weight'] = np.random.randn(num_features, 1)
    weights['Bias'] = np.random.randn(1, 1)

    return weights
```

### Forward Pass

In the forward pass, the neural network is evaluated to generate predicitons from the dot product of inputs to a layer and the model weights. The output of this is then summed with the bias for each layer before being passed through an activation function.

The activation function introduces non-linearity to an otherwise linear relationship between inputs and model weights.

```python
def forward_pass(X_batch: np.ndarray,
                 y_batch: np.ndarray,
                 weights: Dict[str, np.ndarray]) -> Tuple[float, Dict[str, np.ndarray]]:
    # Sanity Check: Batch sizes of X and y are equal
    assert X_batch.shape[0] == y_batch.shape[0]

    # Sanity Check: Matrices have dimensions allowing dot product
    assert X_batch.shape[1] == weights['Weight'].shape[0]
    
    # Sanity Check: Bias is an ndarray of dimensions (1, 1)
    assert weights['Bias'].shape[0] == weights['Bias'].shape[1] == 1

    # Forward pass
    N: np.ndarray = np.dot(X_batch, weights['Weight'])
    P: np.ndarray = N + weights['Bias']
    P: np.ndarray = sigmoid(P)

    # Loss calculation
    loss: float = compute_rmse(P, y_batch)

    # Storing results in dictionary
    forward_info: Dict[str, np.ndarray] = {}
    forward_info['X'] = X_batch
    forward_info['N'] = N
    forward_info['P'] = P
    forward_info['y'] = y_batch

    return (loss, forward_info)
```

### References

[[1] Sajid Sarker, *Evaluating Predictive Models*. Blog Post, 2023.](https://sajidsarker.github.io/2023/02/09/evaluating-predictive-models.html)

[[2] Sajid Sarker, *Activation Functions*. Blog Post, 2023.](https://sajidsarker.github.io/2023/02/27/activation-functions.html)
