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
### MATLAB
``` matlab
% Observer design
lambda = [-0.5 -0.6 -0.5+0.5i -0.5-0.5i]; % poles
P_obsv_d = exp(5*lambda*Ts);
L = place(F',C',P_obsv_d)'
% Finding the continous time eigenvalues
log(eig(F-L*C))/Ts
```