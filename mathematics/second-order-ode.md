# Second Order ODE

<script type="text/javascript" src="../js/general.js"></script>

### Solve in Matlab
---

* solve 2nd order differential equation :　$$\frac{d^{2}x}{dt^{2}} +５\frac{dx}{dt}-4x(t) = sin(10t)$$, and initial x(0) = 0 and x'(0) = 0

* Derivation

assume $$x_{1} = x, x_{2} = x'$$

$$=> x_{1}' = x', x_{2}' = x''$$

$$=> x_{2} = x_{1}'$$ and $$x_{2}' + 5x_{1}' -4x = sin(10t)$$

$$=> x_{1}' = x_{2}$$ and $$x_{2}' = -5x_{1}' + 4x + sin(10t) = -5x_{2} + 4x_{1} + sin(10t) $$

then the above 2 first order ODE would be further solved on matlab code

* matlab code

```matlab
function second_order_ode
    % solv : d2x/dt2 + 5 dx/dt - 4 x = sin (10t)
    % init : x(0) = 0, x'(0) = 0
    
    t = 0:0.01:3
    init_x = 0;
    init_dxdt = 0;
    
    [t, x] = ode45(@rhs, t, [init_x init_dxdt]);
    plot(t, x(:,1));
    xlabel('t');
    ylabel('x');
    
    % two first order ode implemented
    function dxdt = rhs(t, x)
        dxdt_1 = x(2);
        dxdt_2 = -5*x(2) + 4*x(1) + sin(10*t);
        
        dxdt = [dxdt_1; dxdt_2];
    end
end
```

* the result

![](../images/second-order-ode.jpg)

### Solve in Python
---

* solve 2nd order differential equation : $$(3x-1)\frac{d^{2}y}{dt^{2}}-(3x+2)\frac{dy}{dt}-(6x-8)y = 0$$, and initial y(0) = 2, y'(0) = 3

```python
import numpy as np
import scipy as sp
from scipy.integrate import odeint
import matplotlib.pyplot as plt

def g(y, x):
    y0 = y[0]
    y1 = y[1]
    y2 = ((3*x+2)*y1 + (6*x-8)*y0)/(3*x-1)
    return y1, y2

# Initial conditions on y, y' (x=0)
init = 2.0, 3.0

# integrate from 0 to 2
x = np.linspace(0,2,100)
sol = odeint(g, init, x)
plt.plot(x, sol[:,0], color='b')

# integrate from 0 to -2
x = np.linspace(0,-2,100)
sol = odeint(g, init, x)
plt.plot(x, sol[:,0], color='b')

# The analytical answer in red dots
exact_x = np.linspace(-2,2,10)
exact_y = 2*np.exp(2*exact_x)-exact_x*np.exp(-exact_x)
plt.plot(exact_x,exact_y, 'o', color='r', label='exact')
plt.legend()

plt.show()
```

* the result

![](../images/second-order-ode-python.jpg)
