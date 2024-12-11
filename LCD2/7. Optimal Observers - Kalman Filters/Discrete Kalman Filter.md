Also known as $\textbf{linear quadratic estimation (lqe)}$.
## $\texttt{kalman()}$ vs $\texttt{dlqe()}$
### $\texttt{dlqe()}$
Works only for discrete time systems. Returns Kalman gain **L** for state estimation.
```matlab
[L, P, E] = dlqe(A, G, C, Q, R)
```
- **`A`**: State matrix
- **`G`**: Noise distribution matrix (often equal to `B` if process noise acts through the same channels as control input)
- **`C`**: Measurement matrix
- **`Q`**: Process noise covariance matrix
- **`R`**: Measurement noise covariance matrix
- **`L`**: Kalman gain
- **`P`**: Error covariance matrix
- **`E`**: Estimator poles (eigenvalues of the estimation error dynamics)
### $\texttt{kalman()}$
Works for continuous and discrete systems. Returns a state-space modle $\texttt{kest}$ that represents the Kalman filter. Should be easily combined with other state-space systems for simulation and control design.
```matlab
[kest, L, P] = kalman(sys, Q, R, N, Ts)
```
- **`sys`**: State-space system (continuous or discrete)
- **`Q`**: Process noise covariance matrix
- **`R`**: Measurement noise covariance matrix
- **`N`**: Cross-covariance (optional, typically `0`)
- **`Ts`**: Sampling time (`0` for continuous-time, `Ts` for discrete-time)
- **`kest`**: State-space model of the Kalman filter
- **`L`**: Kalman gain
- **`P`**: Error covariance matrix
## E22 Kalman filter implementation
### Step-by-Step Explanation

1. **State-Space Model Setup**:  
    Since `kalman()` works with state-space models, you need to create a state-space system using `ss()`. In this context:
    - **`F`**: State transition matrix (discrete-time version of `A`).
    - **`G`**: Input matrix for the process noise.
    - **`C`**: Output matrix.
    
1. **Process and Measurement Noise Covariances**:
    - **`V1d`**: Discrete-time process noise covariance matrix.
    - **`V2d`**: Discrete-time measurement noise covariance (scalar in your case).
    
2. **System Matrices for Kalman Filter**:  
    For the `kalman()` function, the process noise input matrix should match the dimensions of `F` and `C`.
    
1. **Design the Kalman Filter**:  
    Call `kalman()` to get the state-space model of the Kalman filter and the Kalman gain `L`.
    
1. **Simulate and Use the Filter**:  
    The resulting Kalman filter model can be used to estimate the state vector given noisy measurements.
### Matlab
```matlab
% Given Parameters
Ts = 0.01;  % Sampling time

% State-space matrices
F_KF = F;     % State transition matrix
G_KF = G;     % Input matrix for control input
C_KF = C;     % Output matrix
Gv_KF = eye(4); % Process noise input matrix (identity for process noise)

% Process noise covariance matrix (discrete-time)
V1 = diag([0.00001 0.000001 0.00001 0.000001]);
Bv = diag([F(1,1) 1 F(3,3) 1]);  % Noise enters feedback of theta_dot and x_dot
V1d = Bv * V1 * Bv' * Ts;

% Measurement noise covariance (discrete-time)
noise_ampl = 0.005;
V2 = (noise_ampl / 3)^2;
V2d = V2 / Ts;

% Create the state-space model for the system
sys = ss(F_KF, Gv_KF, C_KF, 0, Ts);

% Design the Kalman filter using the kalman() function
[kest, L_KF, P] = kalman(sys, V1d, V2d);

% Display the Kalman gain
disp('Kalman Gain L_KF:');
disp(L_KF);

% Display the error covariance matrix
disp('Error Covariance P:');
disp(P);
```
#### Code explanation
- **System Matrices**:
    
    - `F_KF`: State transition matrix for the discrete system.
    - `Gv_KF`: Identity matrix indicating that process noise affects all states.
- **Noise Covariances**:
    
    - **Process Noise (`V1d`)**: Derived from the continuous `V1` and scaled by the sampling time `Ts`.
    - **Measurement Noise (`V2d`)**: Scaled by `Ts` to match discrete-time requirements.
- **State-Space System**:
    
    - The system `sys` is defined with `F_KF`, `Gv_KF`, `C_KF`, and the sampling time `Ts`.
- **Kalman Filter Design**:
    
    - **`kest`**: State-space model of the Kalman filter.
    - **`L_KF`**: Kalman gain.
    - **`P`**: Steady-state error covariance.
#### Output interpretation
- **`kest`**: This is a state-space model representing the Kalman filter. It can be used directly in simulations.
- **`L_KF`**: The Kalman gain used to update the state estimate based on measurement errors.
- **`P`**: Represents the steady-state error covariance matrix, indicating the uncertainty in the state estimates.
#### Practical use
To simulate the filter and estimate the states, you can combine the `kest` model with your system model in MATLAB:
```matlab
% Simulate the system with the Kalman filter
t = 0:Ts:10;  % Simulation time
u = randn(size(t));  % Simulated input (process noise)

% Simulate system output with noise
y = lsim(sys, [u;u;u;u], t) + sqrt(V2d) * randn(length(t), size(C_KF, 1));

% Estimate states using the Kalman filter
x_est = lsim(kest, y, t);

% Plot estimated states
figure;
plot(t, x_est);
xlabel('Time (s)');
ylabel('State Estimates');
title('State Estimation using Kalman Filter');
legend('State 1', 'State 2', 'State 3', 'State 4');

```
$\texttt{[u;u;u;u]}$ because the dimensions must match the $n$-number of input channels. In the example $\texttt{sys.B = eye(4)}$, so we need a 4-column $\texttt{u}$.