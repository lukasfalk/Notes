## Set-point tracking
The term $N$ is a pre-compensator gain that adjusts the control input so the system can track a reference input correctly.
``` matlab
N = inv(C * inv(eye(4) - (F - G * K_opt)) * G);
```
