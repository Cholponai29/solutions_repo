```
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Constants
G = 6.67430e-11  # m^3/kg/s^2
M = 5.972e24     # kg (mass of Earth)
R_earth = 6.371e6  # m (radius of Earth)

# Earth's escape velocity at the surface
v_escape = np.sqrt(2 * G * M / R_earth)

# Initial conditions
altitude = 300e3  # 300 km above Earth's surface
r0 = R_earth + altitude
initial_positions = np.array([r0, 0.0])  # starting at (r0, 0)
angles = [0, 45, 90]  # in degrees
speeds = [7.5e3, v_escape, 12e3]  # various initial speeds (m/s)

# Time span for simulation
t_max = 8000  # seconds
t_eval = np.linspace(0, t_max, 10000)

def gravity_ode(t, y):
    rx, ry, vx, vy = y
    r = np.sqrt(rx**2 + ry**2)
    ax = -G * M * rx / r**3
    ay = -G * M * ry / r**3
    return [vx, vy, ax, ay]

# Plot setup
plt.figure(figsize=(8, 8))
earth = plt.Circle((0, 0), R_earth, color='blue', alpha=0.3, label='Earth')
ax = plt.gca()
ax.add_patch(earth)

# Simulate and plot each trajectory
for speed in speeds:
    for angle_deg in angles:
        angle_rad = np.radians(angle_deg)
        vx0 = speed * np.cos(angle_rad)
        vy0 = speed * np.sin(angle_rad)
        y0 = [r0, 0, vx0, vy0]

        sol = solve_ivp(gravity_ode, [0, t_max], y0, t_eval=t_eval, rtol=1e-8)
        rx, ry = sol.y[0], sol.y[1]

        # Filter values inside Earth's radius to stop the plot
        mask = np.sqrt(rx**2 + ry**2) >= R_earth
        rx, ry = rx[mask], ry[mask]

        plt.plot(rx, ry, label=f'{speed/1000:.1f} km/s @ {angle_deg}°')

# Plot customization
plt.xlabel('x (m)')
plt.ylabel('y (m)')
plt.title('Payload Trajectories near Earth')
plt.axis('equal')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```
