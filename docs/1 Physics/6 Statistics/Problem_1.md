```
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Set random seed for reproducibility
np.random.seed(42)

# Parameters
population_size = 100000  # Population size for each distribution
sample_sizes = [5, 10, 30, 50]  # Sample sizes for sampling distribution
n_samples = 1000  # Number of samples to take for each sample size

# Simulate populations
uniform_population = np.random.uniform(0, 1, population_size)
exponential_population = np.random.exponential(scale=1, size=population_size)
binomial_population = np.random.binomial(n=10, p=0.5, size=population_size)

# Function to create sample means for different sample sizes
def sample_means(population, sample_size, n_samples):
    means = []
    for _ in range(n_samples):
        sample = np.random.choice(population, size=sample_size, replace=True)
        means.append(np.mean(sample))
    return means

# Plotting function for histograms
def plot_sampling_distribution(population, dist_name, sample_sizes, n_samples):
    plt.figure(figsize=(14, 10))
    for i, sample_size in enumerate(sample_sizes, 1):
        sample_mean_dist = sample_means(population, sample_size, n_samples)
        plt.subplot(2, 2, i)
        sns.histplot(sample_mean_dist, kde=True, stat='density', bins=30)
        plt.title(f'{dist_name} Distribution\nSample Size = {sample_size}')
        plt.xlabel('Sample Mean')
        plt.ylabel('Density')
    plt.tight_layout()
    plt.show()

# Plot sampling distributions for all types of populations
plot_sampling_distribution(uniform_population, 'Uniform', sample_sizes, n_samples)
plot_sampling_distribution(exponential_population, 'Exponential', sample_sizes, n_samples)
plot_sampling_distribution(binomial_population, 'Binomial', sample_sizes, n_samples)
```

