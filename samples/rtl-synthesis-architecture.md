# EDA System Architecture: RTL-to-GDSII Synthesis Flow

## Overview
This architectural guide outlines the end-to-end automated synthesis pipeline for converting Register-Transfer Level (RTL) HDL code into an optimized gate-level netlist (GDSII flow). It details data model ingestion, logical optimization stages, and static timing constraints required for timing closure in modern silicon design.

---

## 1. Pipeline Data Model & Inputs

Before initiating synthesis, the execution engine validates three core input data structures:

| Data Input | Format / Extension | Description |
| :--- | :--- | :--- |
| **RTL Source** | `.v`, `.sv`, `.vhd` | Hardware Description Language files defining design logic. |
| **Timing Constraints** | `.sdc` (Synopsys Design Constraints) | Clock definitions, input/output delays, and false paths. |
| **Technology Libraries** | `.lib`, `.db` | Target foundry process rules, cell propagation delays, and power models. |

---

## 2. Core Synthesis Execution Stages
### Stage 1: Elaboration & Parsing
* Translates high-level behavioral HDL into intermediate boolean logic representations.
* Checks design hierarchy and validates register inferencing.

### Stage 2: Target-Independent Optimization
* Performs dead-code elimination, constant propagation, and boolean equation simplification.
* Optimizes resource allocation without foundry-specific parameters.

### Stage 3: Technology Mapping & Timing Closure
* Maps generic boolean gates to specific standard cells provided in the technology `.lib`.
* Evaluates setup ($t_{\text{setup}}$) and hold ($t_{\text{hold}}$) slack constraints:
  $$\text{Slack}_{\text{setup}} = T_{\text{required}} - T_{\text{arrival}}$$
* Automatically inserts buffers or resizes gates to eliminate negative slack violations.

---

## 3. Automated Error & Verification Checks
The synthesis engine executes automated checks before emitting the final netlist:
* **Undriven Inputs:** Flags uninitialized wire connections.
* **Combinational Loops:** Identifies un-clocked feedback loops causing race conditions.
* **Multi-Driven Nets:** Detects short-circuit conditions across parallel logic drivers.
