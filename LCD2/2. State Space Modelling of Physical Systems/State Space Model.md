### Continuous Time Model (CTM)
![[Pasted image 20240916174650.png]]


![[Pasted image 20240916174805.png]]
```matlab
[V, D] = eig(A)
```

### Discrete Time Model (DTM)
Most correct notation:
$$\textbf{x}((k+1)T) = \textbf{Fx}(kT) + \textbf{Gu}(kT),$$
$$\textbf{y}(kT) = \textbf{Cx}(kT) + \textbf{Du}(kT)$$
Which can be simplified to:
$$\textbf{x}(k+1) = \textbf{Fx}(k) + \textbf{Gu}(k),$$
$$\textbf{y}(k) = \textbf{Cx}(k) + \textbf{Du}(k)$$
Or even:
$$\textbf{x}_{(k+1)} = \textbf{Fx}_k + \textbf{Gu}_k,$$
$$\textbf{y}_k = \textbf{Cx}_k + \textbf{Du}_k$$
