...
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # Gravitational constant (m^3 kg^-1 s^-2)
M = 5.972e24     # Mass of Earth (kg)

# Generate a range of orbital radii (in meters)
radii = np.linspace(7e6, 4.2e7, 100)  # from 7,000 km to 42,000 km

# Calculate orbital periods for circular orbits
def orbital_period(r, M):
    return 2 * np.pi * np.sqrt(r**3 / (G * M))

periods = orbital_period(radii, M)

# Plot T^2 vs r^3
T_squared = periods**2
r_cubed = radii**3

plt.figure(figsize=(8, 5))
plt.plot(r_cubed, T_squared, label=r"$T^2$ vs $r^3$", color='navy')
plt.xlabel(r"Orbital Radius Cubed $r^3$ (m$^3$)")
plt.ylabel(r"Orbital Period Squared $T^2$ (s$^2$)")
plt.title("Kepler's Third Law: $T^2 \propto r^3$")
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

# Optional: Show a linear fit to confirm proportionality
from scipy.stats import linregress
slope, intercept, r_value, *_ = linregress(r_cubed, T_squared)

print(f"Fitted slope (should be ~4π²/GM): {slope:.3e}")
print(f"R² value: {r_value**2:.5f} (should be close to 1)")
...
