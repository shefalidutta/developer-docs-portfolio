# CLI API Reference: `eda-cli`

`eda-cli` is a command-line interface for orchestrating Electronic Design Automation (EDA) workflows, including logic synthesis, Static Timing Analysis (STA), Design Rule Checking (DRC), and artifact export.

---

## Global Options

Global options apply to all `eda-cli` commands.

| Option | Short | Type | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `--config` | `-c` | `string` | `./eda.config.json` | Path to custom workspace configuration file. |
| `--verbose` | `-v` | `boolean` | `false` | Enables verbose logging output to `stdout`. |
| `--json` | `-j` | `boolean` | `false` | Formats command output as a JSON payload. |
| `--help` | `-h` | `boolean` | `false` | Displays help information for the executed command. |

---

## Command Overview
### Supported Commands

* [**`init`**](#eda-cli-init) – Initialize a new project directory structure.
* [**`build`**](#eda-cli-build) – Synthesize and compile design source files.
* [**`analyze`**](#eda-cli-analyze) – Execute Static Timing Analysis (STA) and Design Rule Checks (DRC).
* [**`export`**](#eda-cli-export) – Generate production artifacts (e.g., GDSII, LEF/DEF).

---

## Command Details

### `eda-cli init`

Initializes an EDA workspace with standard directory structures, baseline configuration templates, and environment settings.

#### Syntax
#### Arguments

* **`project-name`** *(string, required)* – Target project folder name to create.

#### Options

* **`--template, -t `** *(string, optional)* – Project template to seed the build environment. Supported options: `rtl-std`, `analog-basic`, `mixed-signal`. Default: `rtl-std`.
* **`--force, -f`** *(boolean, optional)* – Overwrites existing files in target directory if present.

#### Example
---

### `eda-cli build`

Executes logic synthesis and generates netlist binaries based on workspace RTL source code.

#### Syntax
#### Options

* **`--target `** *(string, optional)* – Target build phase (`synthesis`, `place-and-route`, `all`). Default: `all`.
* **`--threads `** *(integer, optional)* – Number of parallel execution threads. Default: `4`.
* **`--out `** *(string, optional)* – Output directory path for generated build files. Default: `./dist`.

#### Output Structure

Upon successful completion, artifacts are structured as follows:
#### Example
---

### `eda-cli analyze`

Runs static timing analysis and rule enforcement checks against compiled netlists.

#### Syntax
#### Options

* **`--rule-set `** *(string, required)* – Path to the rule enforcement definition file (`.drc` or `.tcl`).
* **`--max-violations `** *(integer, optional)* – Maximum allowed violation count before exiting with failure. Default: `0`.

#### Example
---

## Exit Codes

`eda-cli` returns standard POSIX exit status codes:

| Code | Status | Description |
| :--- | :--- | :--- |
| `0` | **`OK`** | Command executed without errors. |
| `1` | **`ERR_SYNTAX`** | Syntax error, missing required arguments, or invalid options. |
| `2` | **`ERR_CONFIG`** | Missing or corrupt `eda.config.json` workspace file. |
| `127` | **`ERR_DRC_VIOLATION`** | Build or analysis failed due to DRC/timing constraints exceeding limits. |
