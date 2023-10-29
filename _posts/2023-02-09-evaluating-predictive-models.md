---
layout: post
title: Evaluating Predictive Models
date: 2023-02-09 15:22:00
tags: [Artificial Intelligence, Data Science, Mathematics, Python, Machine Learning, Statistics]
---
## Evaluating Predictive Models

Optimising predictive models based on linear relationships often requires minimising the vertical Euclidean distance between predictions and actual observations drawn from a population of unknown distribution.

There are various ways of calculating this distance (or difference). These metrics are generally defined as **residuals**, and allows us to gauge the accuracy of a predictive model or estimator.

Different disciplines, such as statistics or machine learning, refer to residuals using different terms. Popularly, they are referred to as residuals, errors, or loss.

The lower the residual for predictions made on sample data, the less likely the predictions are considered erroneous and the better the performance is of the model.

### Computing Mean Absolute Error (MAE)

The **Mean Absolute Error** is calculated as the average of the absolute difference between predictions and actual observations.

$$MAE = \frac{1}{n} \sum_{i=1}^{n}\begin{vmatrix}y_i-\hat{y}_i\end{vmatrix}$$

```python
def compute_mae(predictions: np.ndarray, actuals: np.ndarray) -> float:
    return np.mean(np.abs(predictions-actuals))
```

However, this function is not continuous nor differentiable at 0, posing a challenge in the computation of loss gradients.

Additionally, the residual is scaled according to the data, making it difficult to compare the accuracy of predictive models with residuals computed on differently scaled data.

### Computing Mean Bias Error (MBE)

The **Mean Bias Error** is calculated as the average of the difference between predictions and actual observations.

$$MBE = \frac{1}{n} \sum_{i=1}^{n}(y_i-\hat{y}_i)$$

```python
def compute_mbe(predictions: np.ndarray, actuals: np.ndarray) -> float:
    return np.mean(predictions-actuals)
```

It's an intuitive measure for understanding the direction of the loss. A negative residual would indicate predictions are generally overstated compared to a positive residual indicating the converse.

It is, however, a poor measure of the magnitude of the error in question, making it show consistently incorrect values in a particular direction.

### Computing Mean Squared Error (MSE)

The **Mean Squared Error** calculates the average of the squared difference between predictions and actual observations.

$$MSE = \frac{1}{n} \sum_{i=1}^{n}(y_i-\hat{y}_i)^2$$

```python
def compute_mse(predictions: np.ndarray, actuals: np.ndarray) -> float:
    return np.mean(np.power(predictions-actuals, 2))
```

Unlike **MAE**, the **MSE** is non-negative, continuous, and differentiable, making it well-suited for optimisation. However, the problems of data scaling persists.

This residual can penalise large differences as a property of the square term. The double-edged sword is that the impact of outliers disproportionately balloons the degree of error.

### Computing Root Mean Squared Error (RMSE)

This is the same as **MSE**, but we take the square root of the mean of the squared difference in predictions and actual observations.

$$RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n}(y_i-\hat{y}_i)^2}$$

```python
def compute_rmse(predictions: np.ndarray, actuals: np.ndarray) -> float:
    return np.sqrt(np.mean(np.power(predictions-actuals, 2)))
```

### Computing Coefficient of Determination (R<sup>2</sup>)

The **Coefficient of Determination (R<sup>2</sup>)** is a statistical measure assessing the 'goodness of fit' in a predictive model.

$$R^2 = 1 - \frac{\sum_{i=1}^{n}(y_i-\hat{y}_i)^2}{\sum_{i=1}^{n}(y_i-\bar{y}_i)^2}$$

```python
def compute_rsquare(predictions: np.ndarray, actuals: np.ndarray) -> float:
    return 1 - ( np.sum(np.power(predictions-actuals, 2)) / np.sum(np.power(np.mean(predictions)-actuals, 2)) )
```

R<sup>2</sup> quantifies the proportion of the variance in the dependent variable that can be explained by the independent variables.

In other words, R<sup>2</sup> indicates how well a model explains the variation in the observed data. Usually, R<sup>2</sup> lies between 0 and 1, where 0 indicates that variation in the dependent variable cannot be explained by the independent variables, and 1 implies perfect predictability by the independent variables.

### Computing Adjusted Coefficient of Determination (Adj. R<sup>2</sup>)

$$R^2 (adj.) = 1 - (\frac{n-1}{n-k-1} * (1-R^2))$$

```python
def compute_adj_rsquare(predictions: np.ndarray, actuals: np.ndarray) -> float:
    n = predictions.shape[0]
    k = predictions.shape[1]
    return 1 - ( ((1 - compute_rsquare(predictions, actuals)) * (n - 1)) / (n - k - 1) )
```

### References

[[1] Aurélien Géron, *Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow: Concepts, Tools, and Techniques to Build Intelligent Systems*. California: O'Reilly Media, 2019.](https://www.amazon.com/Hands-Machine-Learning-Scikit-Learn-TensorFlow/dp/1492032646)

[[2] Hastie, Trevor, Robert, Tibshirani and J. H. Friedman, *The Elements of Statistical Learning: Data Mining, Inference, and Prediction*. New York: Springer, 2009.](https://www.amazon.com/Elements-Statistical-Learning-Prediction-Statistics/dp/0387848576)
