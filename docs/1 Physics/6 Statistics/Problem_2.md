```
import numpy as np
import matplotlib.pyplot as plt

# Part 1: Circle-based Monte Carlo Method

def estimate_pi_circle(n_points):
    # Generate random points in the square (-1, 1)
    x = np.random.uniform(-1, 1, n_points)
    y = np.random.uniform(-1, 1, n_points)

    # Count how many points fall inside the unit circle
    inside_circle = (x**2 + y**2) <= 1
    # Estimate pi
    pi_estimate = 4 * np.sum(inside_circle) / n_points
    
    return pi_estimate, x, y, inside_circle

# Part 2: Buffon's Needle Method

def estimate_pi_buffon(needle_length, line_spacing, n_drops):
    # Count how many times the needle crosses a line
    crossings = 0
    for _ in range(n_drops):
        # Random angle of needle with respect to lines
        angle = np.random.uniform(0, np.pi / 2)
        # Random distance from the center of the needle to the nearest line
        distance_to_line = np.random.uniform(0, line_spacing / 2)
        
        # Check if the needle crosses a line
        if distance_to_line <= (needle_length / 2) * np.sin(angle):
            crossings += 1
    
    # Estimate pi using Buffon's Needle formula
    pi_estimate = (2 * needle_length * n_drops) / (crossings * line_spacing)
    
    return pi_estimate, crossings

# --- Circle-based Monte Carlo Simulation ---
n_points = 10000  # Number of random points for the Monte Carlo estimate
pi_estimate, x, y, inside_circle = estimate_pi_circle(n_points)

# Visualization for Circle-based Method
plt.figure(figsize=(8, 8))
plt.scatter(x[inside_circle], y[inside_circle], color='blue', s=1, label='Inside Circle')
plt.scatter(x[~inside_circle], y[~inside_circle], color='red', s=1, label='Outside Circle')
plt.gca().set_aspect('equal', adjustable='box')
plt.title(f'Estimate of Pi = {pi_estimate:.4f} using Monte Carlo (Circle Method)')
plt.xlabel('x')
plt.ylabel('y')
plt.legend()
plt.show()

# --- Buffon's Needle Simulation ---
needle_length = 1  # Length of the needle
line_spacing = 2  # Distance between lines
n_drops = 10000  # Number of needle drops

pi_estimate_buffon, crossings = estimate_pi_buffon(needle_length, line_spacing, n_drops)

# Display Buffon's Needle Estimate
print(f"Estimate of Pi using Buffon's Needle = {pi_estimate_buffon:.4f}")

```
