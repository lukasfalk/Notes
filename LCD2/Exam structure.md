READ THE FULL PROBLEM DESCRIPTION, YOU MORON
# Numerical Exercise
1. [[Stationary Point & Linearization|Point of stationarity and linearization]] ($\texttt{trim()}, \texttt{linmod()}$)
2. Internal and external [[Stability|stability]] ( $\texttt{eig()}, \texttt{poles()}$ )

Choose yourself from here. Do 3 & 4 or 5 & 6. Not connected.

3. Control design
   - [[Controllability and Observability#Controllability|Controllability]] test (controllability matrix)
   - [[Discretization|Discretize system]](sampling time Ts, $\texttt{c2d()}$)
   - Architecture
   - [[Designing LQR|LQR]] or arbitrary eigenstructure assignment ([[Full-state Feedback|full-state feedback]])
4. Implementation of controller
   - Closed loop linear model (livescript)
   - Closed loop nonlinear model (simulink)
5. Kalman filtering
   - Address architecture of kalman filter. Adjust and/or expand model to account for demands.
   - [[Controllability and Observability#Observability|Observability]] analysis (observability matrix)
   - Present $V_1, V_2$
   - Design kalman filter (always discrete time)
6. Implementation and verification of kalman filter
   - Implementation on design model (linear)
   -> Verification: { Plotting of state estimates vs the true values of the states,
				Comparison of the numerical estimation  error covariances vs the theoretical one,
				Autocorrelation of the innovation signal $y-\hat y$ }
   - Implementation on nonlinear model
   -> Repeat verification

Hand-ins:
Live script and simulink.
Should be able to run seemingly