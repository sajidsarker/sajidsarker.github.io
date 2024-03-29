---
layout: post
title: Activation Functions
date: 2023-02-27 11:10:00
tags: [Artificial Intelligence, Data Science, Deep Learning, Machine Learning, Mathematics, Neural Networks, Python, Statistics]
---
## Activation Functions

In an extension of my previous post on **neural networks**, I will be detailing the different activation functions used to transform the dot product of our input matrix and weights (parameters), as observations are fed forward through the different layers in a network during training.

Activation functions covered are those most popularly used.

### Sigmoid

Non-linear relationship, but requires additive computational burden between layers.

```python
def sigmoid(x):
    return 1 / (1 + np.exp(-x))
```

### Rectified Linear Units (ReLU)

Linear relationship, requiring lower computational burden between layers.

```python
def relu(x):
    return x if x > 0 else 0
```

### Leaky ReLU

An adjustment to the ReLU function given an epsilon small enough.

```python
def leaky_relu(x, epsilon=0.01):
    return x if x > 0 else x * epsilon
```

### Hyperbolic Tangent (Tanh)

This function is perfectly degenerate, being a wrapper for an established NumPy function that calculates the element-wise hyperbolic tangent (*don't @ me*).

However, an alternate and differentiable expression does exist.

```python
def tanh(x):
    return np.tanh(x)

def tanh(x):
    return (np.exp(x) - np.exp(-x)) / (np.exp(x) + np.exp(-x))
```

### Exponential Linear Unit (ELU)

Monotone exponential relationship for negative values that are scaled downwards.

```python
def elu(x, epsilon=1.0):
    return x if x > 0 else epsilon * (np.exp(x) - 1)
```

### Swish

A combined transformation dependent on the sigmoid function.

```python
def swish(x):
    return x * sigmoid(x)
```

### Softmax

This activation function is critical for multi-class classification models.

```python
def softmax(x):
    exp_x = np.exp(x - np.max(x))
    return exp_x / np.sum(exp_x)
```
