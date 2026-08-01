# Shefali Dutta | Developer Documentation Portfolio

Welcome! I am **Shefali**, a Senior Technical Writer specializing in Electronic Design Automation (EDA) software, hardware developer platforms, and chip design toolchains.

---

## 💡 About Me & Technical Domain

With a foundational background as an **SoC Design Engineer** combined with **Technical Writing**, I bridge the gap between complex silicon design pipelines and intuitive developer documentation. 

### Core Capabilities
* **Hardware & EDA Concepts:** RTL Synthesis, Static Timing Analysis (STA), Design Rule Checking (DRC), TCL/SDC scripting, and foundry technology libraries (`.lib`).
* **Docs-as-Code Workflows:** Git, GitHub Actions, Markdown/MDX, static linters (`markdownlint`), automated link validation (`lychee`), and static site generators.
* **Information Architecture:** Structured reference docs, CLI API specs, step-by-step developer onboarding, and conceptual system architecture guides.

---

## 📂 Featured Portfolio Samples

The table below outlines the featured samples available in the [`samples/`](./samples/) directory:

| Sample Document | Category | Key Highlights & Focus Areas |
| :--- | :--- | :--- |
| **[`quickstart-guide.md`](./samples/quickstart-guide.md)** | **Developer Onboarding** | Step-by-step environment setup, licensing configuration, and end-to-end synthesis execution flow. |
| **[`cli-api-reference.md`](./samples/cli-api-reference.md)** | **CLI Reference** | Complete command-line interface specification for `eda-cli`, including global flags, subcommands, and POSIX exit codes. |
| **[`tcl-command-reference.md`](./samples/tcl-command-reference.md)** | **Scripting API Reference** | Formal TCL command API reference for static timing constraints (`create_clock`) and path queries (`get_timing_paths`). |
| **[`sdc-timing-constraints.md`](./samples/sdc-timing-constraints.md)** | **Hardware Concepts Guide** | Conceptual guide covering SDC clock domains, generated clocks, and Clock Domain Crossing (CDC) exceptions. |
| **[`troubleshooting-eda-builds.md`](./samples/troubleshooting-eda-builds.md)** | **Troubleshooting & Diagnostics** | Diagnostic matrix, root-cause analyses, and resolution procedures for build & license failures. |
| **[`rest-api-reference.md`](./samples/rest-api-reference.md)** | **REST API Reference** | Complete OpenAPI/REST API reference covering HTTP methods, Bearer authentication, JSON schemas, and `curl` snippets. |
| **[`release-notes.md`](./samples/release-notes.md)** | **Release & Migration** | Enterprise release notes, breaking API change migration guides, and Semantic Versioning (SemVer) changelogs. |
| **[`rtl-synthesis-architecture.md`](./samples/rtl-synthesis-architecture.md)** | **System Architecture** | Conceptual architecture guide detailing RTL-to-gate mapping pipelines and intermediate representations. |
| **[`rtl-synthesis-architecture-mermaid.md`](./samples/rtl-synthesis-architecture-mermaid.md)** | **Visual Architecture** | Interactive Mermaid.js flowchart and sequence diagram edition of the RTL synthesis pipeline. |

---

## 📁 Repository Directory Structure

```text
developer-docs-portfolio/
├── .github/
│   └── workflows/
│       └── docs-ci.yml                 # CI/CD pipeline for markdown linting & link checking
├── samples/                            # Production documentation samples
│   ├── quickstart-guide.md             # Developer quickstart & onboarding
│   ├── cli-api-reference.md            # CLI flags & subcommand API spec
│   ├── tcl-command-reference.md       # Scripting command reference (SDC/TCL)
│   ├── sdc-timing-constraints.md      # Conceptual guide for SDC & CDC exceptions
│   ├── troubleshooting-eda-builds.md  # Troubleshooting & error resolution guide
│   ├── rest-api-reference.md          # REST API & OpenAPI Developer Reference
│   ├── release-notes.md               # Enterprise Release Notes & Migration Guide
│   ├── rtl-synthesis-architecture.md  # Conceptual architecture guide
│   └── rtl-synthesis-architecture-mermaid.md # Diagrammatic/Visual edition (Mermaid.js)
└── README.md                           # Main portfolio landing page
```

## 📬 Contact & Professional Links
* **Author:** Shefali Dutta
* **LinkedIn:** [linkedin.com/in/shefali-dutta-0185a9175](https://www.linkedin.com/in/shefali-dutta-0185a9175)
* **Email:** [dutta2000shefali@gmail.com](mailto:dutta2000shefali@gmail.com)
