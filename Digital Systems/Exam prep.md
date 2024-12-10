
## Problem 1
### Q 1.1
Mealy(a): outputs depends on state and input.
Moore(b): outputs depends on state.
![[mealy vs moore.png]]

### Q 1.2
They are mealy, as there is a signal from input, directly to the output LUTs:
![[Synthesised Circuit.png]]
### Q 1.3
A LUT is a layer of DFFs that remembers the inputs and then there is cascading number of 2:1 MUXs. A 3LUT:
![[3LUT.png]]
n DFFs = n inputs
### Q 1.4
``` VHDL
entity DFF is
	port(
	D : in std_logic;
	Q : out std_logic;
	reset : in std_logic;
	clk : in std_logic;
	);
end DFF;

architecture Behavior of DFF is
	begin
	process(clk)
		begin
		if rising_edge(clk) then
			if reset = '1' then
				Q <= '0';
			else
				Q <= D;
			end if;
		end if;
	end process;
end Behavior
```
## Problem 2
### Q 2.1
Slowest path, from DFF to DFF:
DFF -> LUT4 -> DFF
$$T_{clk}\ge t_{prop, DFF} + t_{prop, LUT} + t_{SU, DFF} =$$
$$T_{clk,min} = 400\ ps + 600\ ps + 250\ ps = 1250\ ps$$
### Q 2.2
$$ T_{clk} - T{clk,min} \ge 2\cdot \delta$$
$$ \frac{2000 - 1250}{2}=375\ge\delta$$
## Problem 3
### Q 3.1
Longest path:
A -> B -> C -> D -> G -> J -> K
$L=1+2+3+4+3+2+1=16\ ns$
$T=\frac{1}{15\ ns}$
### Q 3.2

## Problem 4
### Q 4.1
