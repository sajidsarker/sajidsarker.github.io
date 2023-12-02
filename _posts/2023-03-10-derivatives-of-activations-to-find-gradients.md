---
layout: post
title: Derivatives of Activations to find Gradients
date: 2023-03-10 18:47:00
tags: [Artificial Intelligence, Data Science, Deep Learning, Mathematics, Neural Networks, Python, Machine Learning, Statistics]
---
## Derivatives of Activations to find Gradients

In an extension of my previous post on **neural networks**, I will be detailing the different derivatives generated for activation functions. These derivatives produce the necessary gradients during backwards propagation with which we may update our weights (parameters), as our errors are fed backwards through the different layers in a network during optimisation.

Derivatives of activation functions covered are those most popularly used.

### Sigmoid

```python
def gradient_sigmoid(x):
    return (1 / (1 + np.exp(-x))) * ( 1 - (1 / (1 + np.exp(-x))))
```

### Rectified Linear Units (ReLU)

```python
def gradient_relu(x):
    return 1 if x > 0 else 0
```

### Leaky ReLU

An adjustment to the ReLU function given an epsilon small enough.

```python
def gradient_leaky_relu(x, epsilon=0.01):
    return 1 if x > 0 else epsilon
```

### Hyperbolic Tangent (Tanh)

This function is similarly degenerate, being a wrapper for an established NumPy function that calculates the element-wise hyperbolic tangent.

However, an alternate and differentiable expression does exist.

```python
def gradient_tanh(x):
    return 1 - np.tanh(x)**2

def gradient_tanh(x):
    return 1 - (np.exp(x) - np.exp(-x)) / (np.exp(x) + np.exp(-x))**2
```

### Exponential Linear Unit (ELU)

```python
def gradient_elu(x, epsilon=1.0):
    return 1 if x > 0 else epsilon * np.exp(x)
```

### Swish

```python
def gradient_swish(x):
	return (x * np.exp(-x) + 1 + np.exp(-x)) / (1 + np.exp(-x))**2
```
