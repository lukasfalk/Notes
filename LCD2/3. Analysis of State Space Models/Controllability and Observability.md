## Lecture 11
### Controllability
If a system is controllable, all the the columns of controllability matrix $Mc$ is linearly independent. If they are linearly independent the inverse of $P$ exists.
Controllability Theorem CC2:
```MATLAB
Mc = ctrb(A,B);

% Test if the controlabillity matrix has at least as many
% linearly independant columns as the number of states in the system:
if rank(Mc) >= size(A,1)
	disp('System is controllable!');
else
	disp('System is NOT controllable!');
end
```
#### Canonical form
```MATLAB
% In Matlab, the useage of the poly() function is shown
chapo = poly(A)
% Here the P matrix is defined from determining the p vectors
p1 = B;
p2 = A*p1 + chapo(2)*p1;
p3 = A*p2 + chapo(3)*p1;
p4 = A*p3 + chapo(4)*p1;
P = [p4 p3 p2 p1]
% By using the P matrix the system can be written in the controller
% canonical form
Acc = P^(-1)*A*P
```

### Observability
Observability Theorem OC2:
```MATLAB
Mo = obsv(A,C);

% Test if the observability matrix has full column rank,
% and if the system is therefore observable.
if rank(Mo) >= size(A,1)
	disp('System is observable!');
else
	disp('System is NOT observable!');
end
```
If observable, design [[Observer|observer]].
