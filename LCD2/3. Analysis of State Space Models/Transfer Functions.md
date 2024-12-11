The poles/eigenvalues, $p_i$ can be real or complex. If real, the system will have a time constant :$$\tau_i=-\frac{1}{p_i}$$
## [[State Space Model|SS]] to TF
``` matlab
[num, den] = ss2tf(A,B,C,D) % numerator and denumenator from SS model
G = minreal(tf(num, den)) % minimum terms of TF
```
## Eigenmodes / natural modes
Find the symbolic eigemodes
```matlab
syms t
function eigenmode = eigmode(A,r,t)
% 'A' is state matrix, 'r' how many decimals and 't' is time
	eigen = eig(A);
	eigenmode = sym([]);
	for x = 1:length(eigen)
		eigen_val = round(vpa(eigen(x)), r);
		eigenmode(end + 1) = exp(eigen_val * t);
	end
end
```
More on frequency properties in [[Frequency Properties]].