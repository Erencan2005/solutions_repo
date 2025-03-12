# Problem 2
# Investigating the Dynamics of a Forced Damped Pendulum

## Motivation

The forced damped pendulum is a captivating example of a physical system exhibiting intricate behavior due to the interplay of damping, restoring forces, and external periodic forces. By introducing damping and external forcing, the system transitions from simple harmonic motion to a rich spectrum of dynamics, including resonance, chaos, and quasiperiodic behavior. These phenomena provide insights into real-world systems, such as driven oscillators, climate models, and mechanical structures under periodic stress.

Adding forcing introduces new parameters, such as the amplitude and frequency of the external force, which significantly affect the pendulum's behavior. Systematic variations in these parameters reveal synchronized oscillations, chaotic motion, and resonance phenomena. These behaviors highlight fundamental physics principles and provide engineering insights into energy harvesting, vibration isolation, and mechanical resonance.

## Task

### 1. Theoretical Foundation

#### Governing Equation
The motion of a forced damped pendulum is described by the differential equation:

\[ \frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \sin \theta = F_0 \cos(\omega t) \]

where:
- \(\theta\) is the angular displacement,
- \(\gamma\) is the damping coefficient,
- \(\omega_0\) is the natural frequency,
- \(F_0\) is the amplitude of the external force,
- \(\omega\) is the driving frequency.

#### Approximate Solutions for Small-Angle Oscillations
For small angles (\(\theta \approx \sin\theta\)), the equation simplifies to:

\[ \frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \theta = F_0 \cos(\omega t) \]

Solving this using standard techniques yields solutions representing driven damped harmonic oscillations.

#### Resonance Conditions
Resonance occurs when the driving frequency \(\omega\) matches the system’s natural frequency \(\omega_0\), leading to energy amplification. The impact of damping on resonance behavior and its practical implications in engineering are discussed.

### 2. Analysis of Dynamics

- Influence of the damping coefficient, driving amplitude, and frequency on motion.
- Transition from periodic to chaotic motion.
- Physical interpretations of regular and chaotic motion, explored via phase portraits and bifurcation diagrams.

### 3. Practical Applications

- **Energy Harvesting**: Mechanical resonance in energy collection devices.
- **Suspension Bridges**: Understanding resonance-induced structural failures.
- **Oscillating Circuits**: Analogies to driven RLC circuits.

### 4. Implementation

#### Computational Model
Using Python, we numerically solve the forced damped pendulum equation using the Runge-Kutta method and visualize the results.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Define the forced damped pendulum equation
def forced_damped_pendulum(t, y, gamma, omega0, F0, omega):
    theta, omega_t = y
    dydt = [
        omega_t,
        -gamma * omega_t - omega0**2 * np.sin(theta) + F0 * np.cos(omega * t)
    ]
    return dydt

# Parameters
gamma = 0.2  # Damping coefficient
omega0 = 1.0  # Natural frequency
F0 = 0.5  # Driving force amplitude
omega = 0.8  # Driving frequency

time_span = (0, 50)  # Simulation time
initial_conditions = [0.1, 0]  # Initial theta and angular velocity
time_eval = np.linspace(*time_span, 1000)

# Solve the differential equation
solution = solve_ivp(
    forced_damped_pendulum, time_span, initial_conditions, t_eval=time_eval, 
    args=(gamma, omega0, F0, omega)
)

# Plot the results
plt.figure(figsize=(10, 5))
plt.plot(solution.t, solution.y[0], label="Theta (rad)")
plt.xlabel("Time (s)")
plt.ylabel("Angular Displacement (rad)")
plt.title("Forced Damped Pendulum Motion")
plt.legend()
plt.grid()
plt.show()
```

#### Visualization
- Time evolution of \(\theta(t)\) for different parameters.
- Phase diagrams illustrating different motion regimes.
- Poincaré sections and bifurcation diagrams to explore chaotic behavior.

## Deliverables

1. **Markdown document** with explanations and Python implementations.
2. **Graphical representations** of motion under varying conditions.
3. **Discussion on model limitations** and potential extensions, such as nonlinear damping and non-periodic driving forces.
4. **Phase portraits and bifurcation diagrams** for understanding transitions to complex dynamics.

## Hints and Resources

- Use small-angle approximations where valid.
- Apply numerical techniques (Runge-Kutta) for beyond-small-angle exploration.
- Relate the pendulum dynamics to driven RLC circuits and biomechanics.
- Utilize Python for simulations and visualizations.

This study bridges theoretical analysis and computational exploration, fostering a deeper understanding of forced and damped oscillatory phenomena in physics and engineering.

![alt text](image-2.png)