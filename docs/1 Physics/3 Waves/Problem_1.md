```
import numpy as np
import matplotlib.pyplot as plt

# Wave parameters
A = 1             # amplitude
wavelength = 1.0  # meters
frequency = 1.0   # Hz
omega = 2 * np.pi * frequency
k = 2 * np.pi / wavelength
phi = 0  # same phase for all sources

# Simulation grid
grid_size = 400
x = np.linspace(-5, 5, grid_size)
y = np.linspace(-5, 5, grid_size)
X, Y = np.meshgrid(x, y)

# Polygon setup
def generate_polygon_vertices(sides, radius):
    angles = np.linspace(0, 2*np.pi, sides, endpoint=False)
    return np.stack([radius * np.cos(angles), radius * np.sin(angles)], axis=1)

# Choose polygon type
polygon_sides = 5  # Try 3 for triangle, 4 for square, etc.
radius = 2.5
sources = generate_polygon_vertices(polygon_sides, radius)

# Time snapshot
t = 0  # try different values for animation

# Superposition of waves
U = np.zeros_like(X)
for x0, y0 in sources:
    R = np.sqrt((X - x0)**2 + (Y - y0)**2)
    U += A * np.cos(k * R - omega * t + phi)

# Plotting the interference pattern
plt.figure(figsize=(8, 8))
plt.pcolormesh(X, Y, U, shading='auto', cmap='RdBu')
plt.colorbar(label='Wave Displacement')
plt.scatter(sources[:, 0], sources[:, 1], color='black', label='Sources')
plt.title(f'Wave Interference from {polygon_sides} Sources (Regular Polygon)')
plt.xlabel('x (m)')
plt.ylabel('y (m)')
plt.axis('equal')
plt.legend()
plt.grid(False)
plt.tight_layout()
plt.show()
```


