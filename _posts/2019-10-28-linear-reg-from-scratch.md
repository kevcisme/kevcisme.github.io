---
layout: post
title: Linear Regression from Scratch
---

If you're diligently following along, you may have seen that I'm doing a series on machine learning models from scratch.

If you aren't, here's the [link to the kickoff post.](https://kevcisme.github.io/new-cohort/)

I'm starting out with Linear Regression (LR). I'll move from a simpler example to a more optimized implementations. Throughout this, you'll get a better intuition of LR and times where it's an appropriate model choice.

First, let's start with a linear equation:
```
y = 2x + 3
```
Depending on the value of `x` that you plug in, you'll receive a varying output, `y`. If you plot out the x and y numbers on a Cartesian plane, you'll see that this equates to a line.

Now let's see that with some examples. Let's say we're trying to predict the sales for our ice cream shop, based on the temperature. We've anecdotally gathered that as the temperature goes up, our sales go up as well. We'll take our input data: `x`, which is the temperature data we collected for a number of days, and then look at the corresponding output data, `y`, our sales. Our model in this instance will be a linear one. We're assuming that there is a line that we could draw - as x goes up, y goes up in a linear fashion.

We're making an assumption about the world, and we're taking a complex situation like our sales and mapping that to a linear input/output. Interestingly enough though, lots of phenomenon follow a linear pattern. You might already have a correct assumption here though: on some days, it's likely to be really hot, and we'll have low sales, and on some days, it's likely to be colder, and we'll have high sales. If this exceeds some threshold, we usually call these events outliers. However, over a long enough period of time, these events probably balance each other out. This was the motivation behind LR when it was first created. Gauss and Legendre published methods known as least squares (which we'll get into under metrics) in 1809 and 1805 respectively. Francis Galton coined the term `regression` to describe a biological phenomenon: heights of descendants of tall ancestors tend to regress down toward a normal average. This regressing pattern is known as a regression to the mean. In this, we can think of the ice cream store and our data that doesn't fit the exact linear pattern - the mean is going to describe the general space where we expect our sales to be, given our temperature.
Let's translate that to code.

We'd like to first find the mean of group of numbers. Let's make some coding assumptions that we might have a basic Python list, or we might have more advanced data type like a Numpy Array or Pandas Series.

This function should handle for all three scenarios.

```
def _get_mean(ind_variable):
    """Calculates the mean of a series of data"""
    return sum(ind_variable) / len(ind_variable)
```

Next, we need to calculate the variance of our data from the mean. By finding the variance of our data points from the mean, we're getting an understanding of how "far away" our data points are.
```
def _get_variance(ind_variable):
    mean = _get_mean(ind_variable)
    mean_difference_square = [(datapoint_x - mean)**2 for datapoint_x in ind_variable]
    variance = sum(mean_difference_square)/float(len(ind_variable)-1)
    return variance
```

Next, we want to calculate covariance. We do this because covariance is a measurement of how two variables move. As our x moves, how does our y move? You can think of this as an unstandardized version of correlation. Here, we create a covariance score between an independent variable and our dependent variable. In our example, temperature is the independent variable and sales is the dependent variable.

After finding the mean of our independent and dependent variables, we loop through the length of the number of items that exist and:
1. Subtract the mean of all values from our data points of the independent variable.
2. Subtract the mean of all values from our data points of the dependent variable.
3. Multiply those two values together.
4. Add the resulting product to a variable we're calling `covariance.`

Then after we have that value, covariance, we divide by the number of items we have (or number of rows or observations) which is subtracted by 1 because stats stuff.

```
def _get_covariance(ind_variable, dep_variable):
    ind_variable_mean = _get_mean(ind_variable)
    dep_variable_mean = _get_mean(dep_variable)
    how_many_datapoints = len(ind_variable)
    covariance = 0.0
    for i in range(how_many_datapoints):
        covariance += (ind_variable[i] - ind_variable_mean) * (dep_variable[i] - dep_variable_mean)
    return covariance / float(how_many_datapoints - 1)
```
Sweet. Now we're able to calculate LR. We're going to assume a Pandas dataframe. We're also assuming a single column for each!


```
def linear_regression(dataframe, ind_var, dep_var):

    # Define X and y for quick reference
    X = dataframe[ind_var]
    y = dataframe[dep_var]

    # Find the means   
    ind_mean = _get_mean(X)
    dep_mean = _get_mean(y)

    # Find the variance of X and y
    ind_variance = _get_variance(X)
    dep_variance = _get_variance(y)

    # Find the covariance of our independent and dependent variable
    covariance = _get_covariance(X, y)

    # Find our Beta Coefficients
    b1 = covariance           
    b0 = dep_mean - b1 * ind_mean

    # Create our Prediction
    prediction = b0 + b1 * X

    return prediction
  ```


## Metrics
How far off is our model?

Great question! We need to know how far away from ground truth our model is.
It's most helpful if this value represents our error in one of two ways:

1. How far off are all of our predictions in the aggregate?
2. Given a prediction, how far off will our model be?

Let's start with the first.

Remember how Gauss called his model "least squares?" The intuition for our aggregate metric is found in the title. We want to create a model whose squared error is the least or lowest amount possible.

We'll take the difference between our predicted value and the actual value, and square it. Then, we'll take the mean of all of these values. Why do we square it? Because we're masochists who love to see our predictions fail by a lot.

```
def mse(actual_value, predicted_value):
    squared_errors = [(predicted_value[i] - actual_value[i])**2 for i in range(len(predicted_value))]

    return sum(squared_errors) / len(squared_errors)

```

## Optimizing
Now that we've gained an intuition on LR and how we can calculate how far off our model is, we can explore ways to optimize. Here, optimization takes two forms:
1. Computational optimization:
  - What is the fastest speed that we can find those Beta values?
  - What is the least memory intensive way to compute?
  - How do we ensure accuracy of our computations?
  - Can we scale the computing operations out? Can we parallelize any of the computations?
2. Can we iteratively optimize our Beta values such that we end up with our best possible model, during the model training process?
