# Second Order ODE

<script type="text/javascript" src="../js/general.js"></script>

### Solve in Matlab
---

* solve 2nd order differential equation :　$$\frac{d^{2}x}{dt^{2}} +５\frac{dx}{dt}-4x(t) = sin(10t)$$, and initial x(0) = 0 and x'(0) = 0

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
    
    function dxdt = rhs(t, x)
        dxdt_1 = x(2);
        dxdt_2 = -5*x(2) + 4*x(1) + sin(10*t);
        
        dxdt = [dxdt_1; dxdt_2];
    end
end
```

* the result



### Solve in Python
---

* solve 2nd order differential equation : $$(3x-1)\frac{d^{2}y}{dt^{2}}-(3x+2)\frac{dy}{dt}-(6x-8)y = 0$$, and initial y(0) = 2, y'(0) = 3
