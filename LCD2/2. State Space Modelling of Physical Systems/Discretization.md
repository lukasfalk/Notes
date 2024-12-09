State and input matrix transformations:
$[\textbf{A}, \textbf{B}]$ -> $[\textbf{F}, \textbf{G}]$
Integrator is Z:
$\int$ -> $Z^{-1}$
MATLAB scripts for [[State Space Model#Discrete Time Model (DTM)|discretizing a state space model]]
```MATLAB
% Discrete system
Ts = 0.1;
[F,G] = c2d(A,B,Ts);
```