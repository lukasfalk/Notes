
## Matlab functions
$\texttt{trim()}$ finds the stationary point.
$\texttt{linmod()}$ linearizes the model around the stationary point.
### E23 - stationary point and linearization
``` MATLAB
x0 = [10; 0];
u0 = 0;
y0 = [0 0];
[xss, uss, yss, dx] = trim(SIMULINK_FILENAME, x0, u0, y0, [1], [], [])
[A,B,C,D] = linmod(SIMULINK_FILENAME, xss, uss)
```