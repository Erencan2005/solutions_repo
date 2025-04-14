# Problem 1
# Exploring the Central Limit Theorem through Simulations

## Table of Contents
1. **Introduction**
2. **Simulating Sampling Distributions**
3. **Sampling and Visualization**
4. **Parameter Exploration**
5. **Practical Applications**
6. **Python Code Implementation**

---

## 1. Introduction

The **Central Limit Theorem (CLT)** is a cornerstone of probability and statistics. It states that, given a sufficiently large sample size $ n $, the sampling distribution of the sample mean approaches a normal distribution, regardless of the shape of the original population distribution. Mathematically:

$$
\bar{X} \sim \mathcal{N}\left(\mu, \frac{\sigma^2}{n}\right)
$$

where:
- $ \bar{X} $: Sample mean
- $ \mu $: Population mean
- $ \sigma^2 $: Population variance
- $ n $: Sample size

In this exploration, we will simulate the CLT using various population distributions (Uniform, Exponential, Binomial) and observe how the sampling distribution of the sample mean converges to normality as $ n $ increases.

---

## 2. Simulating Sampling Distributions

We will simulate data from the following population distributions:
- Uniform Distribution
- Exponential Distribution
- Binomial Distribution

For each distribution, we generate a large dataset representing the population.

---

## 3. Sampling and Visualization

We randomly sample data from the population and calculate the sample mean for different sample sizes ($ n = 5, 10, 30, 50 $). This process is repeated multiple times to create a sampling distribution of the sample mean. Histograms are plotted to visualize the convergence to normality.

---

## 4. Parameter Exploration

We investigate:
- How the shape of the original distribution affects the rate of convergence.
- The impact of the population's variance on the spread of the sampling distribution.

---

## 5. Practical Applications

The CLT has numerous real-world applications, including:
- Estimating population parameters with confidence intervals.
- Quality control in manufacturing processes.
- Predicting outcomes in financial models.

---

## 6. Python Code Implementation
![alt text](image.png)


```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Set random seed for reproducibility
np.random.seed(42)

# Function to simulate sampling distribution of the sample mean
def simulate_clt(population, sample_sizes, num_samples=1000):
    for n in sample_sizes:
        sample_means = [np.mean(np.random.choice(population, size=n)) for _ in range(num_samples)]
        plt.figure(figsize=(8, 4))
        sns.histplot(sample_means, kde=True, bins=30, color='blue')
        plt.title(f'Sampling Distribution (n={n})')
        plt.xlabel('Sample Mean')
        plt.ylabel('Frequency')
        plt.show()

# Generate populations
population_uniform = np.random.uniform(0, 1, size=100000)
population_exponential = np.random.exponential(scale=1, size=100000)
population_binomial = np.random.binomial(n=100, p=0.5, size=100000)

# Define sample sizes
sample_sizes = [5, 10