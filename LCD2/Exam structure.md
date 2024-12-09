# Numerical Exercise
1. Point of stationarity and linearization ($\texttt{trim()}, \texttt{linmod()}$)
2. Internal and external stability ($\texttt{eig()}, \texttt{poles()}$)

Choose yourself from here. Do 4 & 5 or 5 & 6. Not connected.

3. Control design
   - Controllability test (controllability matrix)
   - Discretize system (sampling time Ts, $\texttt{c2d()}$)
   - Architecture
   - LQR or arbitrary eigenstructure assignment
4. Implementation of controller
   - Closed loop linear model (livescript)
   - Closed loop nonlinear model (simulink)
5. Kalman filtering
   - Address architecture of kalman filter. Adjust and/or expand model to account for demands.
   - Observability analysis (observability matrix)
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
Live script and simulink. Should be able to run seemingly