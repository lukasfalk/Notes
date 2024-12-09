Check for [[Controllability and Observability#Observability|observability]] first
SISO system -> ackermann
``` MATLAB
% Calculate gains for full state feedback.
% acker() because we have a SISO system.
K = acker(A, B, lambdas);
```
Newer functions is place():
``` MATLAB
K = place(A, B, poles);
```
Both functions can be used in continuous and discrete time.