
'''
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# System Parameters
gamma = 0.2         # Damping coefficient
omega0 = 1.0        # Natural frequency of the pendulum
A = 1.2             # Amplitude of the external driving force
omega_d = 2/3       # Driving frequency

# Time span for simulation
t_max = 100
t_points = np.linspace(0, t_max, 10000)

# Differential equations for the forced damped pendulum
def forced_damped_pendulum(t, y):
    theta, omega = y
    dtheta_dt = omega
    domega_dt = -gamma * omega - omega0**2 * np.sin(theta) + A * np.cos(omega_d * t)
    return [dtheta_dt, domega_dt]

# Initial conditions: [angle, angular velocity]
y0 = [0.2, 0.0]

# Solve the system using Runge-Kutta method
solution = solve_ivp(forced_damped_pendulum, [0, t_max], y0, t_eval=t_points, method='RK45')

# Extract solution
theta = solution.y[0]
omega = solution.y[1]
time = solution.t

# Normalize angle to be within (-π, π) for better visualization
theta_mod = ((theta + np.pi) % (2 * np.pi)) - np.pi

# Plot: Angle over time
plt.figure(figsize=(10, 4))
plt.plot(time, theta_mod)
plt.xlabel('Time (s)')
plt.ylabel('Angle θ (rad)')
plt.title('Forced Damped Pendulum: Angle over Time')
plt.grid(True)
plt.tight_layout()
plt.show()

# Plot: Phase portrait (θ vs ω)
plt.figure(figsize=(6, 6))
plt.plot(theta_mod, omega, lw=0.5)
plt.xlabel('θ (rad)')
plt.ylabel('ω (rad/s)')
plt.title('Phase Portrait')
plt.grid(True)
plt.tight_layout()
plt.show()

# Plot: Poincaré section (samples taken once every driving period)
T_drive = 2 * np.pi / omega_d
poincare_times = np.arange(0, t_max, T_drive)
theta_poincare = []
omega_poincare = []

for t_cross in poincare_times:
    idx = np.searchsorted(time, t_cross)
    if idx < len(time):
        theta_poincare.append(theta_mod[idx])
        omega_poincare.append(omega[idx])

plt.figure(figsize=(6, 6))
plt.scatter(theta_poincare, omega_poincare, s=5, color='red')
plt.xlabel('θ (rad)')
plt.ylabel('ω (rad/s)')
plt.title('Poincaré Section')
plt.grid(True)
plt.tight_layout()
plt.show()
'''
