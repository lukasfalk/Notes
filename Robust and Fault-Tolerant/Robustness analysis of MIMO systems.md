## Quick notes
$\sigma$ is the singular values of matrix A.
$\underline{\sigma}(A)=\sigma_{min}(A)=\texttt{min}\{\sigma_i\}$
$\bar{\sigma}(A)=\sigma_{max}(A)=\texttt{max}\{\sigma_i\}$

Open loop transfer function $L = GK$
Sensitivity function $S = (I+GK)^{-1}$
Complementary sensitivity function $T = GK(I+GK)^{-1}$

## Singular Value Decomposition (SVD)

## Matrix norms

## $\mu$ (SSV Analysis)
![[Pasted image 20250331222838.png]]
Convoluted AF.
MATLAB code:
```matlab
[bounds,muinfo] = mussv(M,Blockstructure)
% Block structure - important.
[stabmarg,wcu] = robstab(usys)
```
