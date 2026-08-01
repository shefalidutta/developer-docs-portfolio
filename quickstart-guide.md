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
* Configure custom multi-corner timing analyses using custom `.sdc` scripts.
  | Sample File | Category | Description |
| :--- | :--- | :--- |
| [`quickstart-guide.md`](./samples/quickstart-guide.md) | **Onboarding / Guide** | Step-by-step developer quickstart for setting up environments and executing synthesis pipelines. |
| [`cli-api-reference.md`](./samples/cli-api-reference.md) | **API / CLI Reference** | Complete CLI API reference for `eda-cli`, detailing global flags, subcommands, and exit codes. |
| [`rtl-synthesis-architecture.md`](./samples/rtl-synthesis-architecture.md) | **Architecture Guide** | Conceptual architectural overview for RTL logic synthesis pipelines. |
