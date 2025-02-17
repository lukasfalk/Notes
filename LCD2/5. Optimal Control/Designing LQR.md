For LQR vs pole placement, see [[Full-state Feedback#Pole placement or LQR?|Pole placement or LQR?]].
## Discrete time
### Sampling time
```maltab
% Sampling time
T_sett = 25; % selected settling time [s]
tau_sett = T_sett/5; % slowest time constant of closed loop system [s]
tau_ol = 1./abs(lambda_ol(abs(lambda_ol)>0));
Ts_max = min([tau_sett min(tau_ol)]./10) % maximum sampling time [s]
```
### Controller
```matlab
Ts = Ts_max; % 10x smaller than settling time req
[F,G] = c2d(A,B,Ts)
```
Q matrix is the weights for the requirements of the controller. For instance max deviation of angles or settling time deviation in percentages:
```maltab
Q = diag([1/(25^2) 1/(0.05^2)])
```
Now for finding the gain matrix, solution of riccati equation and eigenvaluies:
```matlab
R = 50;
[K_opt,S,lambda_cl_dt] = dlqr(F,G,Q*Ts,R*Ts);
```
Checking stability for Z-domain and complex plane:
```matlab
lambda_cl_dt = abs(lambda_cl_dt) % discrete time / Z-domain
lambda_cl_ct = 1/Ts.*log(lambda_cl_dt) % continous time / complex plane
```
If $abs(\texttt{lambda\_cl\_dt})<1$ => system is stable
For $\texttt{lambda\_cl\_ct}$ see section on [[Stability|stability]].
### Set-point tracking
The term $N$ is a pre-compensator gain that adjusts the control input so the system can track a reference input correctly.
``` matlab
N = inv(C * inv(eye(4) - (F - G * K_opt)) * G);
```
#### Derivation of $N$
In an **LQR (Linear Quadratic Regulator)** design, the goal is to regulate the system to the origin using a state-feedback control law of the form:
$$
u(k) = -K x(k)
$$where:
- \( u(k) \) is the control input at time \( k \),
- \( x(k) \) is the state vector at time \( k \),
- \( K \) is the optimal feedback gain matrix.

This control law minimizes the cost function:
$$
J = \sum_{k=0}^{\infty} \left( x_k^T Q x_k + u_k^T R u_k \right)
$$However, in many practical applications, we want the system to **track a reference set-point**  $r$  rather than just regulate to the origin. To achieve this, we modify the control law to:
$$
u(k) = -K x(k) + N r
$$
where $N$ is the **pre-compensator gain**.
##### Steady-State Condition for Reference Tracking
To determine $N$, we need to ensure that the system output $y(k)$ tracks the reference $r$ at steady state. The system dynamics are given by:
$$
x(k+1) = F x(k) + G u(k)
$$
At steady state, $x(k+1) = x(k) = x_{ss}$ and $u(k) = u_{ss}$. Substituting the control law $u_{ss} = -K x_{ss} + N r$ into the system dynamics:
$$
x_{ss} = F x_{ss} + G (-K x_{ss} + N r)
$$Rearranging:
$$
(I - F + G K) x_{ss} = G N r
$$
###### Ensuring the Output Tracks the Reference
We want the output $y(k)$ to track the reference $r$. Assume the output equation is:
$$
y(k) = C x(k)
$$
At steady state:
$$
y_{ss} = C x_{ss} = r
$$
Substitute $x_{ss} = (I - F + G K)^{-1} G N r$ into the output equation:
$$
C (I - F + G K)^{-1} G N r = r
$$
Cancelling $r$ on both sides:
$$
C (I - F + G K)^{-1} G N = 1
$$
Solving for $N$:
$$
N = \left( C (I - F + G K)^{-1} G \right)^{-1}
$$
##### Final Control Law

The modified control law for set-point tracking becomes:
$$
u(k) = -K x(k) + N r
$$
This ensures that the system output $y(k)$ tracks the reference $r$ without steady-state error.
## Complete design of discrete system
``` MATLAB
[K_opt,S,lambda_cl_dt] = dlqr(F,G,Q*Ts,R*Ts);
lambda_cl_ct = 1/Ts.*log(lambda_cl_dt)
% Set-point control (a solution with integral action would also work here)
N = inv(C*inv(eye(4)-(F-G*K_opt))*G);
sys_cl_dt = ss(F-G*K_opt,G*N,C,D,Ts); % ver2: u = -K_LQR*x + Nr
```
