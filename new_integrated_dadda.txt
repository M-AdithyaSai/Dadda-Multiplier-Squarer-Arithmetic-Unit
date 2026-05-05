library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity full_adder is
    port(
        a, b, cin : in STD_LOGIC;
        sum, cout : out STD_LOGIC
    );
end full_adder;

architecture Behavioral of full_adder is
begin
    sum <= a xor b xor cin;
    cout <= (a and b) or (b and cin) or (cin and a);
end Behavioral;

library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity half_adder is
    port(
        a, b : in STD_LOGIC;
        sum, cout : out STD_LOGIC
    );
end half_adder;

architecture Behavioral of half_adder is
begin
    sum <= a xor b;
    cout <= a and b;
end Behavioral;


library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity approximate_inpreord_4to2_compressor is
    port(
        A, B, C, D, Cin : in STD_LOGIC;
        Sum, Cout, C_int : out STD_LOGIC
    );
end approximate_inpreord_4to2_compressor;

architecture Behavioral of approximate_inpreord_4to2_compressor is
    signal temp_or, temp_or2, A1, B1, C1, D1 : STD_LOGIC;
begin
    -- Approximate logic based on your equations:
    -- Sum = A . ?(B + C + D)
    -- Carry = (B + C) . ?D
    
    A1 <= (A or B) or (C or D);
    B1 <= (A and B) or (C and D);
    C1 <= (A or B) or (C or D);
    D1 <= (A and B) or (C and D);
    
    temp_or <= B1 or C1 or D1;        -- (B + C + D)
    temp_or2 <= B1 or C1;            -- (B + C)
    
    Sum <= A1 and (not temp_or);    -- A . ?(B + C + D)
    Cout <= temp_or2 and (not D1);  -- (B + C) . ?D
    C_int <= D1;                    -- Pass D as internal carry
end Behavioral;

library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity exact_inpreord_4to2_compressor is
    port(
        A, B, C, D, Cin : in STD_LOGIC;
        Sum, Cout, C_int : out STD_LOGIC
    );
end exact_inpreord_4to2_compressor;

architecture Behavioral of exact_inpreord_4to2_compressor is
    signal sum1, carry1, carry2, A1,B1,C1,D1 : STD_LOGIC;
begin
    -- First stage: Add A, B, C
    A1 <= (A or B) or (C or D);
    B1 <= (A and B) or (C and D);
    C1 <= (A or B) or (C or D);
    D1 <= (A and B) or (C and D);
    
    sum1 <= A1 xor B1 xor C1;
    carry1 <= (A1 and B1) or (B1 and C1) or (C1 and A1);
    
    -- Second stage: Add sum1, D, Cin
    Sum <= sum1 xor D1 xor Cin;
    carry2 <= (sum1 and D1) or (D1 and Cin) or (sum1 and Cin);
    
    -- Output carries
    Cout <= carry1;     -- External carry
    C_int <= carry2;    -- Internal carry
end Behavioral;

library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

entity R8AS1_Squarer is
    generic ( N : integer := 8 );
    port ( A : in  STD_LOGIC_VECTOR(N-1 downto 0);
        Y : out STD_LOGIC_VECTOR(2*N-1 downto 0)
    );
end entity;

architecture Behavioral of R8AS1_Squarer is
begin
    process(A)
    begin
    
        Y <= std_logic_vector(signed(A) * signed(A));
        
    end process;
end architecture;


library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity dadda_inpreord_enereff is
 Port (a,b: in std_logic_vector(7 downto 0); y: out std_logic_vector(15 downto 0));
end dadda_inpreord_enereff;

architecture Behavioral of dadda_inpreord_enereff is
signal p: std_logic_vector(63 downto 0);
signal s: std_logic_vector(30 downto 0);
signal c: std_logic_vector(42 downto 0);
signal c1: std_logic_vector(15 downto 0);
signal cin: std_logic;

component full_adder is
port(a,b, cin: in std_logic;
sum, cout: out std_logic);
end component;

component half_adder is 
port(a,b: in std_logic;
sum,cout:out std_logic);
end component;

component exact_inpreord_4to2_compressor is
    port(A, B, C, D, Cin : in STD_LOGIC;
        Sum, Cout, C_int : out STD_LOGIC);
end component;

component approximate_inpreord_4to2_compressor is
    port(A, B, C, D, Cin : in STD_LOGIC;
        Sum, Cout, C_int : out STD_LOGIC);
end component;

begin
cin<='0';
p(0) <= a(0) and b(0);
p(1) <= a(1) and b(0);
p(2) <= a(2) and b(0);
p(3) <= a(3) and b(0);
p(4) <= a(4) and b(0);
p(5) <= a(5) and b(0);
p(6) <= a(6) and b(0);
p(7) <= a(7) and b(0);

p(8) <= a(0) and b(1);
p(9) <= a(1) and b(1);
p(10) <= a(2) and b(1);
p(11) <= a(3) and b(1);
p(12) <= a(4) and b(1);
p(13) <= a(5) and b(1);
p(14) <= a(6) and b(1);
p(15) <= a(7) and b(1);

p(16) <= a(0) and b(2);
p(17) <= a(1) and b(2);
p(18) <= a(2) and b(2);
p(19) <= a(3) and b(2);
p(20) <= a(4) and b(2);
p(21) <= a(5) and b(2);
p(22) <= a(6) and b(2);
p(23) <= a(7) and b(2);

p(24) <= a(0) and b(3);
p(25) <= a(1) and b(3);
p(26) <= a(2) and b(3);
p(27) <= a(3) and b(3);
p(28) <= a(4) and b(3);
p(29) <= a(5) and b(3);
p(30) <= a(6) and b(3);
p(31) <= a(7) and b(3);

p(32) <= a(0) and b(4);
p(33) <= a(1) and b(4);
p(34) <= a(2) and b(4);
p(35) <= a(3) and b(4);
p(36) <= a(4) and b(4);
p(37) <= a(5) and b(4);
p(38) <= a(6) and b(4);
p(39) <= a(7) and b(4);

p(40) <= a(0) and b(5);
p(41) <= a(1) and b(5);
p(42) <= a(2) and b(5);
p(43) <= a(3) and b(5);
p(44) <= a(4) and b(5);
p(45) <= a(5) and b(5);
p(46) <= a(6) and b(5);
p(47) <= a(7) and b(5);

p(48) <= a(0) and b(6);
p(49) <= a(1) and b(6);
p(50) <= a(2) and b(6);
p(51) <= a(3) and b(6);
p(52) <= a(4) and b(6);
p(53) <= a(5) and b(6);
p(54) <= a(6) and b(6);
p(55) <= a(7) and b(6);

p(56) <= a(0) and b(7);
p(57) <= a(1) and b(7);
p(58) <= a(2) and b(7);
p(59) <= a(3) and b(7);
p(60) <= a(4) and b(7);
p(61) <= a(5) and b(7);
p(62) <= a(6) and b(7);
p(63) <= a(7) and b(7);

--stage-1

u1: half_adder port map(p(1),p(8),s(0),c(0));
u2: full_adder port map(p(2),p(9),p(16),s(1),c(1));
u3: approximate_inpreord_4to2_compressor port map(p(3),p(10),p(17),p(24),cin,s(2),c(2),c1(0));
u4: approximate_inpreord_4to2_compressor port map(p(4),p(11),p(18),p(25),cin,s(3),c(3),c1(1));
u5: approximate_inpreord_4to2_compressor port map(p(5),p(12),p(19),p(26),cin,s(4),c(4),c1(2));
u6: approximate_inpreord_4to2_compressor port map(p(6),p(13),p(20),p(27),cin,s(5),c(5),c1(3));
u7: approximate_inpreord_4to2_compressor port map(p(7),p(14),p(21),p(28),cin,s(6),c(6),c1(4));
u8: full_adder port map(p(15),p(22),p(29),s(7),c(7));
u9: half_adder port map(p(23),p(30),s(8),c(8));
u10: half_adder port map(p(33),p(40),s(9),c(9));
u11: full_adder port map(p(34),p(41),p(48),s(10),c(10));
u12: approximate_inpreord_4to2_compressor port map(p(35),p(42),p(49),p(56),cin,s(11),c(11),c1(5));
u13: exact_inpreord_4to2_compressor port map(p(36),p(43),p(50),p(57),cin,s(12),c(12),c1(6));
u14: exact_inpreord_4to2_compressor port map(p(37),p(44),p(51),p(58),cin,s(13),c(13),c1(7));
u15: exact_inpreord_4to2_compressor port map(p(38),p(45),p(52),p(59),cin,s(14),c(14),c1(8));
u16: exact_inpreord_4to2_compressor port map(p(39),p(46),p(53),p(60),cin,s(15),c(15),c1(9));
u17: full_adder port map(p(47),p(54),p(61),s(16),c(16));
u18: half_adder port map(p(55),p(62),s(17),c(17));

--stage-2
u19: half_adder port map(c(0),s(1),s(18),c(18));
u20: half_adder port map(c(1),s(2),s(19),c(19));
u21: full_adder port map(c(2),s(3),p(32),s(20),c(20));
u22: full_adder port map(c(3),s(4),s(9),s(21),c(21));
u23: approximate_inpreord_4to2_compressor port map(c(4),s(5),c(9),s(10),cin,s(22),c(22),c1(10));
u24: approximate_inpreord_4to2_compressor port map(c(5),s(6),c(10),s(11),cin,s(23),c(23),c1(11));
u25: exact_inpreord_4to2_compressor port map(c(6),s(7),c(11),s(12),cin,s(24),c(24),c1(12));
u26: exact_inpreord_4to2_compressor port map(c(7),s(8),c(12),s(13),cin,s(25),c(25),c1(13));
u27: exact_inpreord_4to2_compressor port map(c(8),p(31),c(13),s(14),cin,s(26),c(26),c1(14));
u28: half_adder port map(c(14),s(15),s(27),c(27));
u29: half_adder port map(c(15),s(16),s(28),c(28));
u30: half_adder port map(c(16),s(17),s(29),c(29));
u31: half_adder port map(c(17),p(63),s(30),c(30));

--stage-3--
y(0) <= p(0);
y(1) <= s(0);
y(2) <= s(18);
u32: half_adder port map(c(18),s(19),y(3),c(31));
u33: full_adder port map(c(19),s(20),c(31),y(4),c(32));
u34: full_adder port map(c(20),s(21),c(32),y(5),c(33));
u35: full_adder port map(c(21),s(22),c(33),y(6),c(34));
u36: full_adder port map(c(22),s(23),c(34),y(7),c(35));
u37: full_adder port map(c(23),s(24),c(35),y(8),c(36));
u38: full_adder port map(c(24),s(25),c(36),y(9),c(37));
u39: full_adder port map(c(25),s(26),c(37),y(10),c(38));
u40: full_adder port map(c(26),s(27),c(38),y(11),c(39));
u41: full_adder port map(c(27),s(28),c(39),y(12),c(40));
u42: full_adder port map(c(28),s(29),c(40),y(13),c(41));
u43: full_adder port map(c(29),s(30),c(41),y(14),c(42));
u44: half_adder port map(c(30),c(42),y(15),c1(15));
end Behavioral;

library ieee;
use ieee.std_logic_1164.all;

entity mul_datapath is
    port (
        a, b : in std_logic_vector(7 downto 0);
        y    : out std_logic_vector(15 downto 0)
    );
end mul_datapath;

architecture behavior of mul_datapath is 

    -- Signals for muxed inputs
    signal a_to_mul, b_to_mul : std_logic_vector(7 downto 0);
    signal a_to_sqr           : std_logic_vector(7 downto 0);

    -- Outputs of blocks
    signal yd, ys : std_logic_vector(15 downto 0);

    component dadda_inpreord_enereff is
        port (
            a, b : in std_logic_vector(7 downto 0);
            y    : out std_logic_vector(15 downto 0)
        );
    end component;

    component R8AS1_Squarer is
        generic ( N : integer := 8 );
        port (
            A : in  std_logic_vector(N-1 downto 0);
            Y : out std_logic_vector(2*N-1 downto 0)
        );
    end component;

begin

    -----------------------------------------------------------------
    -- MUX IN FRONT (input selection)
    -----------------------------------------------------------------
    -- If a = b, use squarer → feed only "a" to squarer
    -- If a ≠ b, use multiplier → feed a,b into multiplier

    -- Inputs for multiplier
    a_to_mul <= a when (a /= b) else (others => '0');
    b_to_mul <= b when (a /= b) else (others => '0');

    -- Input for squarer
    a_to_sqr <= a when (a = b) else (others => '0');

    -----------------------------------------------------------------
    -- Instantiations of multiplier & squarer
    -----------------------------------------------------------------
    u1: dadda_inpreord_enereff 
        port map(a => a_to_mul, b => b_to_mul, y => yd);

    u2: R8AS1_Squarer 
        port map(A => a_to_sqr, Y => ys);

    -----------------------------------------------------------------
    -- Output comes from whichever block is active
    -----------------------------------------------------------------
    y <= ys when (a = b) else yd;

end behavior;

