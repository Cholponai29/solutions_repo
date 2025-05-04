# Problem 2

import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # Gravitational constant (m^3/kg/s^2)

# Celestial body data: name, radius (m), mass (kg)
bodies = {
    "Earth": {
        "radius": 6.371e6,
        "mass": 5.972e24
    },
    "Mars": {
        "radius": 3.3895e6,
        "mass": 6.417e23
    },
    "Jupiter": {
        "radius": 6.9911e7,
        "mass": 1.898e27
    }
}

# Functions for cosmic velocities
def first_cosmic_velocity(M, R):
    return np.sqrt(G * M / R)

def second_cosmic_velocity(M, R):
    return np.sqrt(2) * first_cosmic_velocity(M, R)

# Third cosmic velocity estimation from Earth
def third_cosmic_velocity(M_sun, R_earth_orbit):
    return np.sqrt(2 * G * M_sun / R_earth_orbit)

# Compute and display velocities
print("Cosmic Velocities (km/s):\n")
for body, data in bodies.items():
    v1 = first_cosmic_velocity(data["mass"], data["radius"]) / 1000  # km/s
    v2 = second_cosmic_velocity(data["mass"], data["radius"]) / 1000
    print(f"{body}:")
    print(f"  1st Cosmic Velocity: {v1:.2f} km/s")
    print(f"  2nd Cosmic Velocity: {v2:.2f} km/s")

# Estimate 3rd cosmic velocity (from Earth orbit)
R_earth_orbit = 1.496e11  # in meters
M_sun = 1.989e30          # kg
v3 = third_cosmic_velocity(M_sun, R_earth_orbit) / 1000  # km/s

print(f"\nThird Cosmic Velocity (from Earth orbit): {v3:.2f} km/s")

# Visualization
labels = []
v1_vals = []
v2_vals = []

for body, data in bodies.items():
    labels.append(body)
    v1_vals.append(first_cosmic_velocity(data["mass"], data["radius"]) / 1000)
    v2_vals.append(second_cosmic_velocity(data["mass"], data["radius"]) / 1000)

x = np.arange(len(labels))
width = 0.35

plt.figure(figsize=(10, 6))
plt.bar(x - width/2, v1_vals, width, label='1st Cosmic Velocity')
plt.bar(x + width/2, v2_vals, width, label='2nd Cosmic Velocity')
plt.axhline(v3, color='red', linestyle='--', label='3rd Cosmic Velocity (Sun escape)')
plt.xticks(x, labels)
plt.ylabel('Velocity (km/s)')
plt.title('Cosmic Velocities for Various Celestial Bodies')
plt.legend()
plt.grid(True, linestyle='--', alpha=0.6)
plt.tight_layout()
plt.show()
