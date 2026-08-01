# TCL API Reference: Timing Constraints & Path Analysis

This document specifies the TCL scripting commands used to configure static timing constraints and extract timing path metrics within the synthesis and timing analysis engine.

---

## Command Summary

| Command | Category | Description |
| :--- | :--- | :--- |
| [`create_clock`](#create_clock) | **Constraints** | Defines a primary clock object with specified period and waveform. |
| [`set_input_delay`](#set_input_delay) | **Constraints** | Specifies arrival time requirements relative to a reference clock. |
| [`get_timing_paths`](#get_timing_paths) | **Analysis** | Queries and returns a collection of worst-case timing paths. |

---

## Command Specifications

### `create_clock`

Defines a primary clock domain on a top-level port or internal pin, establishing the fundamental timing reference for setup and hold checks.

#### Syntax

```tcl
create_clock -period <period_ns> [-name <clock_name>] [-waveform <edge_list>] <port_pin_list>

# Define a 500 MHz clock (2.0 ns period) with 50% duty cycle on port 'clk_main'
create_clock -period 2.0 -name SYS_CLK [get_ports clk_main]

# Define a clock with an asymmetrical waveform (rising at 0.2ns, falling at 0.8ns)
create_clock -period 1.5 -waveform {0.2 0.8} -name ASYM_CLK [get_ports clk_aux]
get_timing_paths [-delay_type <type>] [-max_paths <int>] [-nworst <int>] [-from <from_list>] [-to <to_list>]

# Extract the 5 worst setup-violating paths from register bank 'reg_a' to 'reg_b'
set critical_paths [get_timing_paths -delay_type max \
                                      -max_paths 5 \
                                      -from [get_cells reg_a*] \
                                      -to [get_cells reg_b*]]

# Iterate over returned path collection and print slack
foreach_in_collection path $critical_paths {
    set slack [get_property $path slack]
    puts "Path Slack: ${slack} ns"
}
