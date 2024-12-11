Full-state feedback is a controller design regarding pole placements. This is also known as the eigenstructure assignment.
## Pole placement or LQR?
### Full-state feedback
Pick full-state feedback if:
- You have a clear ides of where you want the closed loop poles (e.g. settling time, overshoot, damping ratio).
- You want a straightforward control design for a simple system.
- There are no constraints on the magnitude or energy of the input, and you're not concerned about minimizing control effort explicitly.
Pros:
- Intuitive: direct control over closed-loop pole placements.
- Simple to implement: requires solving a linear system for gain matrix $K$.
- Suitable for deterministic systems: Works well when disturbances and noise are minimal or can be ignored.
Cons:
- Trial-and-error: choosing pole locations can sometimes be guesswork or iterative
- Not optimal: does not guarantee optimal performance in terms of balancing speed and control effort.
- May lead to large control effort: if poles are placed too far left in the complex plane (for faster response), it can result in large control signals.
### Optimal control (LQR)
Pick LQR if:
- You want optimal trade-off between system performance(e.g. state error) and control effort. You have a quadratic cost function $J = ∫_0^\infty(x^TQx+u^TRu)dt$ that you want to minimize.
- When minimizing the energy or magnitude of the control input is important. Ideal for systems where actuator limitations, energy efficiency, or control effort constraints are a concern.
- Robustness to modeling errors: LQR tends to be more robust to small modeling errors compared to pole placement.
- Complex or high-order systems: when designing for high-order systems where manually placing poles becomes impractical.
- Stochastic considerations: in cases where the system is subject to disturbances or noise (e.g., when paired with a Kalman filter for LQG control).
Pros:
- Systematic and optimal solution by Riccati equation.
- Automatic trade-off: balances performance and control effort through weighting matrices $Q$ and $R$.
- Scalability, ahndles high-order systems more effectively.
Cons:
- Less intuitive: the relationship between $Q$, $R$, and the resulting pole locations is less direct.
- Tuning difficulty: requires tuning $Q$ and $R$ matrices, which can be challenging and may require trial-and-error.
- Computationally intensive: solves a Riccati equation, which can be more computationally demanding than solving for pole placement gains.
### Summary
| **Criterion**         | **Full-State Feedback (Pole Placement)** | **LQR**                                          |
| --------------------- | ---------------------------------------- | ------------------------------------------------ |
| **Design Goal**       | Specific pole locations                  | Optimal trade-off between performance and effort |
| **Complexity**        | Simpler, intuitive                       | More complex, systematic                         |
| **Control Effort**    | Not explicitly minimized                 | Explicitly minimized                             |
| **Optimality**        | No optimality guarantee                  | Guarantees optimality for quadratic cost         |
| **Tuning**            | Choosing poles manually                  | Tuning `Q` and `R` matrices                      |
| **System Complexity** | Suitable for simple systems              | Suitable for high-order or complex systems       |
| **Robustness**        | Less robust to modeling errors           | More robust to modeling errors                   |
Use full-state feedback when:
- You have straightforward performance requirements (e.g., desired settling time, damping ratio).
- You can easily specify desired pole locations.
- The system is simple, and there are no stringent constraints on control effort.
Use LQR when:
- You need to balance performance and control effort.
- You want a systematic approach to optimal control design.
- The system is complex or high-order.
- Robustness to disturbances or model uncertainties is important.

## Matlab
$\texttt{place()}$
