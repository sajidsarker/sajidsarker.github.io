---
layout: post
title: Neural Network Implementation
date: 2023-03-22 09:36:00
tags: [Artificial Intelligence, Data Science, Machine Learning, Neural Networks, Python, Statistics]
---
## Neural Network Implementation

With fundamentals from past posts on the architecture of **neural networks**, evaluating predictive models, and a look into various activation functions, we can now bring all the elements together.

I'll be detailing a simple implementation of a single layer neural network in Python to toy around with.

![Deep Learning Neural Network](/docs/assets/images/dl.png)

**Figure 1.** *Deep Learning Neural Network with Multiple Layers*

### Libraries

```python
import numpy as np
from typing import Callable, List, Dict, Tuple
```

### Random Initialisation
```python
def initialise_weights(num_features: int) -> Dict[str, np.ndarray]:
    weights: Dict[str, np.ndarray] = {}

    weights['Weight'] = np.random.randn(num_features, 1)
    weights['Bias'] = np.random.randn(1, 1)

    return weights
```

### Forward Pass
```python
def forward_pass(X_batch: np.ndarray,
                    y_batch: np.ndarray,
                    weights: Dict[str, np.ndarray]) -> Tuple[float, Dict[str, np.ndarray]]:
    # Assert batch sizes of X and y are equal
    assert X_batch.shape[0] == y_batch.shape[0]

    # Assert that matrix multiplication can work
    assert X_batch.shape[1] == weights['Weight'].shape[0]
    
    # Assert that B is simply a 1x1 ndarray
    assert weights['Bias'].shape[0] == weights['Bias'].shape[1] == 1

    # Matrix Multiplication
    N = np.dot(X_batch, weights['Weight'])

    # Bias
    P = N + weights['Bias']

    # Calculate Mean Squared Error Loss
    loss = np.mean(np.power(y_batch - P, 2))

    # Save the information computed on the forward pass
    forward_info: Dict[str, np.ndarray] = {}
    forward_info['X'] = X_batch
    forward_info['N'] = N
    forward_info['P'] = P
    forward_info['y'] = y_batch
    
    return forward_info, loss
```
