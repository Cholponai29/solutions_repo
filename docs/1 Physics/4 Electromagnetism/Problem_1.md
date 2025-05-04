```
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants and initial conditions
q = 1.6e-19  # Charge of the particle (C)
m = 9.11e-31  # Mass of the particle (kg)
E = np.array([0, 0, 0])  # Electric field (V/m), zero in simple cases
B = np.array([0, 0, 1])  # Magnetic field (T), aligned with the z-axis
v0 = np.array([1e5, 0, 0])  # Initial velocity (m/s)
r0 = np.array([0, 0, 0])  # Initial position (m)
dt = 1e-9  # Time step (s)
t_max = 1e-6  # Total simulation time (s)

# Time array
t = np.arange(0, t_max, dt)

# Initialize arrays to store particle's position and velocity
r = np.zeros((len(t), 3))  # Position (x, y, z)
v = np.zeros((len(t), 3))  # Velocity (vx, vy, vz)
r[0] = r0
v[0] = v0

# Simulation loop
for i in range(1, len(t)):
    # Calculate Lorentz force
    F = q * (E + np.cross(v[i-1], B))
    # Update velocity and position using Euler's method
    a = F / m
    v[i] = v[i-1] + a * dt
    r[i] = r[i-1] + v[i-1] * dt

# Plot the trajectory in 3D space
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
ax.plot(r[:, 0], r[:, 1], r[:, 2], label="Particle trajectory")
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_zlabel('Z')
ax.set_title('Particle Trajectory in Uniform Magnetic Field')
plt.show()
```


