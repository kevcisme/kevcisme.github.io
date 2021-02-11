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
def _get_mean(observations):
    """Calculates the mean of a series of data"""
    return sum(observations) / len(observations)
```

Next, we need to calculate the variance of our data from the mean. By finding the variance of our data points from the mean, we're getting an understanding of how "far away" our data points are.
```
def _get_variance(observations):
    mean = _get_mean(observations)
    mean_difference_square = [(datapoint_x - mean)**2 for datapoint_x in observations]
    variance = sum(mean_difference_square)/float(len(observations)-1)
    return variance
```
