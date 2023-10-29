---
layout: post
title: Activation Functions
date: 2023-02-27 11:10:00
tags: [Artificial Intelligence, Data Science, Mathematics, Python, Machine Learning, Statistics]
---
## Activation Functions

In an extension of my previous post on **neural networks**, I will be detailing the different activation functions used to transform the dot product of our input matrix and weights (parameters), as observations are fed forward through the different layers in a network during training.

Activation functions covered are those most popularly used, 

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
    return max(0, x)
```

### Leaky ReLU

An adjustment to the ReLU function given an epsilon small enough.

```python
def leaky_relu(x, epsilon=0.01):
    return x if x > 0 else x * epsilon
```

### Hyperbolic Tangent (Tanh)

This function is perfectly degenerate, being a wrapper for an established NumPy function that calculates the element-wise hyperbolic tangent (*don't @ me*).

```python
def tanh(x):
    return np.tanh(x)
```

### Gated Linear Unit (GLU)

A combined transformation dependent on the sigmoid function.

```python
def glu(x, gate):
    return x * sigmoid(gate)
```

### Softmax

This activation function is critical for multi-class classification models.

```python
def softmax(x):
    exp_x = np.exp(x - np.max(x))
    return exp_x / np.sum(exp_x)
```
