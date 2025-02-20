## 5.2 Structural Model

The **Behaviour model** of a system is defined by a pair
	$\mathcal{S} = (\mathcal{C}, \mathcal{Z})$
where
	$\mathcal{Z} = \{\mathcal{z_1}, \mathcal{z_2}, \dotsc, \mathcal{z_N}\}$ is a set of variables and parameters.
	$\mathcal{C} = \{\mathcal{c_1}, \mathcal{c_2}, \dotsc, \mathcal{c_N}\}$ is a set of variables and parameters.
	
The **Structure graph** is represented by a bipartite graph. A graph is bipartite if its set of vertices can be separated into two disjoint sets $\mathcal{C}$ and $\mathcal{Z}$ in such a way that every edge has one endpoint in $\mathcal{C}$ and the other one in $\mathcal{Z}$.
**Definition 5.1** (*Structural model, structure graph*) The *structural model* of the system $\mathcal{S} = (\mathcal{C}, \mathcal{Z})$ is a bipartite graph
	$\mathcal{G} = (\mathcal{C},\mathcal{Z},\mathcal{E})$,
where $\mathcal{E} \subset \mathcal{C} \times \mathcal{Z}$ is the set of edges defined as follows:
	$(c_i, z_j) \in \mathcal{E}$ if the variable $z_j$ appears in the constraint $c_i$.
$\mathcal{G}$ is called the *structure graph* or the *structure*.

**Example 5.3 Structure graph of a linear system**
Consider a linear system described by four constraints $\{c_1, c_2, c_3, c_4\}$ with five variables
$\{x_1, x_2, \dot x_1, \dot x_2, u\}$ as follows:
$$
c_1 : \dot x_1 = \frac{dx_1}{dt}
$$
$$
c_2 : \dot x_1 = ax_2
$$
$$
c_3 : \dot x_2 = \frac{dx_2}{dt}
$$
$$
c_4 : \dot x_2 = bx_1 + cx_2 + du
$$
![[Pasted image 20250212183155.png]]
![[Pasted image 20250212183625.png]]
Constraints are just signals, with each signal being the previous signal(s) with their changes. $c_1, c_2, \dotsc, c_n$
Measurements are just the signals we're probing $m_1, m_2, \dotsc, m_n$
Differentiations are just the the diffs (integrators in simulink) $d_1, d_2, \dotsc, d_n$
Incidence matrices only inlcudes known and unknown variables, not coefficients.
## 5.3 Matching in Bipartite Graphs
$\mathcal{K}$ = known variables
$\mathcal{X}$ = unknown variables
$\mathcal{Z} = \mathcal{K}\cup \mathcal{X}$ (union)

**Definition 5.3** *Matchings* $\mathcal{M}_1, \mathcal{M}_2, \dotsc, \mathcal{M}_n$ are subsets of $\mathcal{E}$ and are disjoint edges of bipartite graph $\mathcal{G}$.

There are more than one *maximum matchings*.
Matching size = is its cardinality $|\mathcal{M}|$.
$|\mathcal{M}|\leq \text{min}\{|\mathcal{C}|, |\mathcal{M}|\}$
*Maximum cardinality* over the set of matchings is called the *matching number* and is denoted by $v(\mathcal{G}) = \text{max}_{\mathcal{M}\in M}|\mathcal{M}|$

**Definition 5.4** (Complete matching) A matching is called complete w.r.t. $\mathcal{C}$ if $|\mathcal{M}| = |\mathcal{C}|$ holds. A matching is called complete w.r.t. $\mathcal{Z}$ if $|\mathcal{M}| = |\mathcal{Z}|$ holds.

Edges of a matching are identified by a thick line in drawings and by encircling the "1"
![[Pasted image 20250212183934.png]]![[Pasted image 20250212183944.png]]

## 5.4 Structural Decomposition of Systems
**Definition 5.6** (*Over-constrained $\mathcal{G}^+$, just-constrained$\mathcal{G}^0$, under-constrained graph$\mathcal{G}^-$*) A graph $\mathcal{G} = (\mathcal{C},\mathcal{Z},\mathcal{E})$ is called
- *over-constrained* if there is a complete matching on the variables $\mathcal{Z}$ but not on the
constraints $\mathcal{C}$.
- *just-constrained* if there is a complete matching on the variables $\mathcal{Z}$ and on the constraints $\mathcal{C}$.
- *under-constrained* if there is a complete matching on the constraints $\mathcal{C}$ but not on the variables $\mathcal{Z}$.
## 5.5 Matching Algorithms
### 5.5.1 Ranking Algorithm
![[Pasted image 20250212190754.png]]
**Algorithm 5.1** *Ranking of the constraints*.
	**Given:** Incidence matrix of a bipartite graph
		1. Mark all known variables with rank 0
		   $i = 1$
		2. Find all constraints in the current table with exactly one unmarked variable. Associate rank $i$ with these constraints and mark these constraints as well as the corresponding variable.
		3. Set $i \mathrel{+}= 1$.
		4. If there are unmarked constraints whose variables are all marked, associate them with rank $i$, mark them and connect them with the pseudo-variable ZERO.
		5. If there are unmarked variables or constraints, continue with Step 2.
	**Result:** Ranking of the constraints.
### 5.5.2 General Matching Algorithm
![[Pasted image 20250212190742.png]]
**Algorithm 5.2** *Algorithm for finding a maximum matching*
	**Given:** A bipartite graph $\mathcal{G}$ and an initial matching $\mathcal{M}_0$ .
		1. Let $\mathcal{M}$ be the current matching. If the number of weak vertices with respect to $\mathcal{M}$ is less than or equal to one, the current matching is maximum. Otherwise, let $v$ be any weak vertex. Build an alternating tree with root $v$.
		2. If the tree contains an $\mathcal{M}$*-augmenting path* then perform a transfer along this path and update the matching on the initial graph.
		   Go back to Step 1.
	**Result:** A maximum matching.
### 5.5.3 Maximum Flow Algorithm
![[Pasted image 20250212190728.png]]
**Algorithm 5.3** *Hungarian method for determining maximum matchings*
	**Given:** A bipartite graph and an initial matching $\mathcal{M}_0$.
		1. Denote the current matching by $\mathcal{M}$. Label with an * all vertices of $\mathcal{Z}$ that are weak with respect to $\mathcal{M}$, and alternately apply Steps 2 and 3 until no further labelling is possible.
		2. Select a newly labelled vertex in $\mathcal{Z}$, say $z_i$, and label with $z_i$ all un-labelled vertices of $\mathcal{C}$ that are connected to $z_i$ by an edge that is weak with respect to $\mathcal{M}$. Repeat this step on all vertices of $\mathcal{Z}$ that were labelled in the previous step.
		3. Select a newly labelled vertex of $\mathcal{C}$, say $c_j$ and label with $c_j$ the vertex of $\mathcal{Z}$ which is connected to $c_j$ in $\mathcal{M}$. Repeat this process on all vertices of $\mathcal{C}$ labelled in the previous step.
		4. The labellings will continue to alternate until one of two possibilities occurs:
	END 1: A weak vertex $\mathcal{C}$ has been labelled. Then an $\mathcal{M}$-augmenting path has been found, and it can be constructed by working backwards through the labels until the vertex of $\mathcal{Z}$ which is labelled by a \*. Transferring this path gives an extended matching and the algorithm is repeated by going back to Step 2.
	END 2: It is not possible to label more vertices and END 1 has not occured. Then $\mathcal{M}$ is a maximum matching.
	**Result:** A maximum matching.
## 5.6 Structural Diagnosability and Isolability
A system is said to be structurally diagnosable or monitorable if it is possible to test whether the system constraints are satisfied or not.
