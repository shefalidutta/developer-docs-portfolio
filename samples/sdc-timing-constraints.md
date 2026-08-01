 # Conceptual Guide: SDC Timing Constraints & Clock Domain Crossing (CDC)

This guide provides a conceptual overview of Synopsys Design Constraints (SDC) used in Static Timing Analysis (STA) to define timing boundaries, clock relationships, and false path exceptions across multi-frequency clock domains.

---

## Overview of Timing Constraints

Static Timing Analysis relies on SDC constraint files to establish timing budgets for setup (max delay) and hold (min delay) checks across a digital circuit. Without explicit constraints, timing engines assume default single-cycle setup relationships between all registers, leading to inaccurate slack calculations.

```text
+-------------------+      SDC Constraints      +-------------------+
|  Unconstrained    | ------------------------> |  Timing Engine    |
|  Netlist (.v)     |   • create_clock          |  Slack Calculation|
|                   |   • set_input_delay       |  (Setup & Hold)   |
+-------------------+   • set_false_path        +-------------------+

# Example: Asynchronous Clock Domains
Clock A (100 MHz):  |___|   |___|   |___|   |___|
Clock B (133 MHz):   |_|  |_|  |_|  |_|  |_|  |_|

# 1. Define Primary System Clock (200 MHz = 5.0 ns period)
create_clock -period 5.0 -name SYS_CLK [get_ports clk_sys]

# 2. Define Generated Divide-by-2 Clock (100 MHz = 10.0 ns period)
create_generated_clock -name SYS_CLK_DIV2 \
                       -source [get_ports clk_sys] \
                       -divide_by 2 \
                       [get_pins u_clk_divider/q_reg/Q]

# 3. Define Asynchronous Clock Boundary Exception
set_clock_groups -asynchronous \
                 -group [get_clocks SYS_CLK] \
                 -group [get_clocks PERIPH_CLK]

# 4. Set Input Arrival Delays relative to SYS_CLK
set_input_delay -max 1.2 -clock SYS_CLK [get_ports data_in[*]]
