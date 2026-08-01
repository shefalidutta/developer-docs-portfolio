# Quickstart Guide: Getting Started with `eda-cli`

This guide walks you through installing `eda-cli`, configuring your local EDA workspace environment, and running your first RTL logic synthesis pipeline from scratch.

---

## Prerequisites

Before starting, ensure your system meets the following software and environment requirements:

| Component | Minimum Version | Notes |
| :--- | :--- | :--- |
| **Operating System** | RHEL / CentOS 8+ or Ubuntu 20.04 LTS | POSIX-compliant Linux environment required. |
| **Python** | `3.9+` | Required for orchestration scripts and TCL interface. |
| **GCC / Clang** | `GCC 10.2+` or `Clang 12.0+` | Essential for compiling C/C++ plugin modules. |
| **License Server** | FlexLM `v11.16+` | Active network access to license server port `27000`. |

---

## Step 1: Install `eda-cli`

Download and install the `eda-cli` executable using the enterprise package manager or direct binary distribution.
Verify that the installation was successful by checking the version output:
**Expected Output:**
---

## Step 2: Configure Environment Variables

Set the required environment paths for your target technology library and license server.

Add the following environment variables to your shell configuration (`~/.bashrc` or `~/.zshrc`):
Reload your shell configuration to apply changes:
---

## Step 3: Initialize a Design Workspace

Use `eda-cli init` to generate a pre-configured design directory structure containing sample RTL source files, synthesis constraint files (`.sdc`), and configuration files.
Navigate into the newly created workspace:
### Generated Project Structure
---

## Step 4: Run Your First Synthesis Build

Execute the logic synthesis workflow to convert your behavioral Verilog code into a technology-mapped gate-level netlist.
### Execution Log Highlights

During execution, `eda-cli` outputs step-by-step pipeline updates:
---

## Step 5: Validate Build Artifacts

Verify that the output directory (`./dist`) contains your compiled netlist and timing reports.
You should see the following generated deliverables:

* **`top_level.v`**: The synthesized gate-level structural Verilog netlist.
* **`reports/synthesis.log`**: Full elaboration and optimization execution logs.
* **`reports/timing_summary.rpt`**: Slack calculation, setup/hold timing report.

---

## Step 6: Run Static Timing & DRC Checks

Run static analysis against your output netlist to verify that there are no setup/hold timing violations or design rule errors.
If analysis passes with zero critical errors, your netlist is ready for physical design (Place and Route).

---

## Next Steps

Now that you have completed your first synthesis build, explore these advanced topics:

* Refer to the [CLI API Reference](./cli-api-reference.md) for full flag descriptions.
* Review the [RTL Synthesis Architecture Overview](./rtl-synthesis-architecture.md) to understand intermediate logic optimizations.
  
## Step-by-Step Onboarding Process

| Step | Action | Command / Output | Description |
| :--- | :--- | :--- | :--- |
| **1. Install `eda-cli`** | Install via package manager | `pip install eda-cli-tools --upgrade` | Downloads and installs the latest stable version of `eda-cli` from the internal registry. |
| **2. Configure Environment** | Export variables in `~/.bashrc` | `export EDA_LICENSE_FILE="27000@lic-server.internal.net"`<br>`export PDK_ROOT="/opt/foundry/pdk/7nm_stdcells"` | Configures paths for active license server access and foundry technology libraries. |
| **3. Initialize Workspace** | Generate project scaffolding | `eda-cli init my_first_design --template rtl-std` | Creates directory structure with sample RTL (`.v`), constraints (`.sdc`), and rules (`.drc`). |
| **4. Run Synthesis** | Execute synthesis engine | `eda-cli build --target synthesis --threads 4` | Synthesizes behavioral Verilog into a technology-mapped gate-level netlist using 4 threads. |
| **5. Validate Artifacts** | Inspect output directory | `ls -la ./dist` | Verifies existence of generated netlist (`top_level.v`), logs, and timing reports (`.rpt`). |
| **6. Run Analysis** | Execute DRC and STA checks | `eda-cli analyze --rule-set ./rules/default.drc` | Analyzes output netlist against foundry constraints to ensure zero timing or rule violations. |
