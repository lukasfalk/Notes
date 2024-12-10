## BIBO stability.
 - The continuous time LTI system (3.37) and (3.53) is BIBO-stable if and only if the poles of the transfer function matrix (3.71) are strictly in the left half plane.
- The discrete time LTI system (3.96) is BIBO-stable if and only if the poles of the transfer function matrix (3.122) are strictly within the unit circle.
## Internal- and external stability.
State space model is an internal model and the stability investigation will determine $\textit{internal stability}$.
Transfer function matrix is the external model and its stability will determine $\textit{external stability}$.
If an unstable eigenvalue/pole is cancelled by a zero, the system may be externally stable although it is internally unstable. An internally stable LTI-system will also be externally stable.
### Matlab
#### Continuous
##### Internal stability
```matlab
[A,B,C,D] = linmod(SIMULINK_FILENAME, xss, uss)
eig(A)
```
If $Re(\lambda_i)<0$ for all eigenvalues, the system is internally stable.
If internally unstable, the system might still be externally stable.
##### External stability
```matlab
[num, den] = ss2tf(A,B,C,D);
G = minreal(tf(num, den))
eigenvalues = pole(G)
```
If $Re(\lambda_i)<0$ for all eigenvalues, the system is externally stable.
#### Discrete
```matlab
[F,G] = c2d(A,B,Ts)
abs(eig(F))
```
If $abs(\texttt{lambda\_cl\_dt})<1$ => system is stable