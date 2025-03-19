# Investigating the Range as a Function of the Angle of Projection

## 1. Theoretical Foundation

### Deriving the Governing Equations

The motion of a projectile can be described by applying Newton's second law. For a projectile launched from an initial position with velocity $v_0$ at an angle $\theta$ with respect to the horizontal, we have:

In the horizontal direction (x-axis):
$$\frac{d^2x}{dt^2} = 0$$

In the vertical direction (y-axis):
$$\frac{d^2y}{dt^2} = -g$$

Where $g$ is the acceleration due to gravity (approximately 9.81 m/s² on Earth).

Integrating these equations with respect to time with initial conditions:
- $x(0) = 0$
- $y(0) = h$ (initial height)
- $v_x(0) = v_0\cos(\theta)$
- $v_y(0) = v_0\sin(\theta)$

We obtain:

$$x(t) = (v_0\cos\theta)t$$
$$y(t) = h + (v_0\sin\theta)t - \frac{1}{2}gt^2$$

These parametric equations describe the position of the projectile at any time $t$.

### Family of Solutions

The family of solutions is defined by varying the parameters:
- Initial velocity ($v_0$)
- Launch angle ($\theta$)
- Initial height ($h$)
- Gravitational acceleration ($g$)

Each combination of these parameters produces a unique trajectory.

## 2. Analysis of the Range

### Range Equation

The range $R$ is the horizontal distance traveled when the projectile returns to its initial height. To find this, we need to determine when $y(t) = h$:

$$h + (v_0\sin\theta)t - \frac{1}{2}gt^2 = h$$

Simplifying:
$$(v_0\sin\theta)t - \frac{1}{2}gt^2 = 0$$

This equation has two solutions: $t = 0$ and $t = \frac{2v_0\sin\theta}{g}$

The second solution gives us the time of flight. The range is then:

$$R = (v_0\cos\theta) \cdot \frac{2v_0\sin\theta}{g} = \frac{v_0^2\sin(2\theta)}{g}$$

This demonstrates that the range is proportional to:
- The square of the initial velocity
- The sine of twice the angle of projection
- Inversely proportional to the gravitational acceleration

### Optimal Angle for Maximum Range

To find the angle that maximizes the range, we differentiate with respect to $\theta$ and set it equal to zero:

$$\frac{dR}{d\theta} = \frac{v_0^2\cos(2\theta)}{g} = 0$$

This gives us $\cos(2\theta) = 0$, thus $2\theta = \frac{\pi}{2}$ or $\theta = \frac{\pi}{4} = 45°$

Therefore, in the absence of air resistance and with a level landing surface, the maximum range is achieved at a 45° angle.

### Effect of Initial Height

If the projectile is launched from a height $h$ above the landing surface, the range equation becomes more complex:

$$R = v_0\cos\theta \cdot t_{landing}$$

Where $t_{landing}$ is the time when the projectile reaches the ground level ($y = 0$):

$$h + (v_0\sin\theta)t_{landing} - \frac{1}{2}gt_{landing}^2 = 0$$

Solving this quadratic equation:

$$t_{landing} = \frac{v_0\sin\theta + \sqrt{(v_0\sin\theta)^2 + 2gh}}{g}$$

This means that the range now depends on the initial height as well:

$$R = v_0\cos\theta \cdot \frac{v_0\sin\theta + \sqrt{(v_0\sin\theta)^2 + 2gh}}{g}$$

## 3. Practical Applications

### Real-world Considerations

In practice, projectile motion is influenced by:
- Air resistance (drag)
- Wind
- Varying gravitational field
- Rotating reference frames (Coriolis effect)
- Non-uniform terrain

### Incorporating Air Resistance

A simple model for air resistance is to include a drag force proportional to velocity:

$$F_d = -bv$$

This leads to a modified set of differential equations:

$$\frac{d^2x}{dt^2} = -\frac{b}{m}v_x$$
$$\frac{d^2y}{dt^2} = -g - \frac{b}{m}v_y$$

Where $b$ is the drag coefficient and $m$ is the mass of the projectile.

These equations typically require numerical methods to solve.

## 4.  pyhton Implementation
![alt text](image-3.png)