# Visual Architecture Guide: RTL Logic Synthesis Pipeline

> **Note:** This document serves as the visual and diagrammatic edition of [`rtl-synthesis-architecture.md`](./rtl-synthesis-architecture.md). It provides native vector flowchart and sequence representations of the Register-Transfer Level (RTL) logic synthesis pipeline for modern Electronic Design Automation (EDA) software suites.

---

## 1. End-to-End Synthesis Pipeline Flowchart

The flowchart below illustrates how behavioral HDL source files transition through high-level elaboration, logic optimization, technology library mapping, and static timing constraints to produce a mapped gate-level netlist.

```mermaid
graph TD
    %% Source Inputs
    subgraph Inputs ["Design Inputs & Target Libraries"]
        A[RTL Source Code<br/>.v / .sv / .vhd]
        C[Technology Library<br/>.lib Standard Cells]
        E[Timing Constraints<br/>.sdc / Clock Definitions]
    end

    %% Core Pipeline Stages
    subgraph CoreEngine ["Synthesis & Optimization Engine"]
        B[Parser & Elaboration Engine]
        G[Logic Optimization &<br/>Boolean Simplification]
        D[Technology Mapping Stage]
        F[Static Timing &<br/>Slack Optimization]
    end

    %% Outputs
    subgraph Outputs ["Build Artifacts & Reports"]
        H[Gate-Level Structural Netlist<br/>.v]
        I[Timing & Slack Summary<br/>.rpt]
        J[Elaboration & Optimization Logs<br/>.log]
    end

    %% Connections
    A --> B
    B -->|Unmapped Intermediate Rep| G
    G --> D
    C --> D
    D --> F
    E --> F
    F --> H
    F --> I
    F --> J

    %% Node Styling
    style A fill:#e1f5fe,stroke:#0288d1,stroke-width:2px
    style C fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    style E fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    style H fill:#e8f5e9,stroke:#388e3c,stroke-width:2px
    style I fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    style J fill:#fff3e0,stroke:#f57c00,stroke-width:2px

sequenceDiagram
    autonumber
    actor Dev as Developer
    participant Driver as Tool Orchestrator
    participant Parser as HDL Parser / Elaborator
    participant LibDB as Liberty (.lib) Database
    participant OptEngine as Logic & Tech Mapper
    participant STA as Timing Engine

    Dev->>Driver: Execute Synthesis Pipeline Command
    Driver->>Parser: Read & Parse RTL Files (.v / .sv)
    activate Parser
    Parser->>Parser: Validate syntax & construct Abstract Syntax Tree (AST)
    Parser->>Parser: Elaborate modules & generate unmapped generic netlist
    Parser-->>Driver: Return generic intermediate representation (IR)
    deactivate Parser

    Driver->>LibDB: Read Target Foundry Cell Definitions (.lib)
    LibDB-->>Driver: Load cell area, delay arcs, and power metrics

    Driver->>OptEngine: Pass IR Netlist + Standard Cell Database
    activate OptEngine
    OptEngine->>OptEngine: Perform Boolean logic optimization & dead code elimination
    OptEngine->>OptEngine: Map generic logic primitives to target technology cells
    OptEngine-->>Driver: Mapped Gate-Level Netlist
    deactivate OptEngine

    Driver->>STA: Read Constraints (.sdc) & Evaluate Slack
    activate STA
    STA->>STA: Compute setup/hold windows & worst negative slack (WNS)
    STA-->>Driver: Return slack calculation metrics & timing logs
    deactivate STA

    Driver-->>Dev: Generate output netlist (.v) & reports (.rpt)
