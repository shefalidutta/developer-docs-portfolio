# Release Notes & Migration Guide: `eda-cli` v2.4.0

**Release Date:** August 2, 2026  
**Target Version:** `v2.4.0` (Upgrading from `v2.3.x`)  
**Compatibility:** Backward-incompatible breaking changes included (requires configuration migration).

---

## 🚀 Release Overview

`eda-cli` v2.4.0 introduces enhanced multi-corner timing optimization, native support for multi-die 3D-IC synthesis pipelines, and significantly faster Static Timing Analysis (STA) path querying. 

This release includes **deprecations and breaking changes** to legacy TCL flag structures and environment configurations to improve pipeline execution safety.

---

## 📌 Summary of Changes

| Category | Summary | Impact |
| :--- | :--- | :--- |
| **New Features** | Multi-die 3D-IC netlist partitioning, parallel STA path engine. | Non-breaking enhancement. |
| **Breaking Changes** | Rename of global `--config` flag; strict JSON schema validation. | **Action required** during upgrade. |
| **Deprecations** | Legacy `create_clock -waveform_legacy` argument deprecated. | Deprecation warning (removal in v3.0). |
| **Bug Fixes** | Fixed memory leak during high-thread synthesis runs. | General improvement. |

---

## 🛑 Breaking Changes & Upgrade Action Items

### 1. Renamed Global Configuration Flag
* **Old Flag:** `--config-file` / `-cf`
* **New Flag:** `--config` / `-c`
* **Reason:** Standardized global options across all CLI toolchains to POSIX standards.

#### Action Required
Update all automated CI/CD shell scripts and Makefile execution targets:

```bash
# ❌ DEPRECATED (v2.3.x)
eda-cli build --config-file ./eda.config.json

# ✅ UPDATED (v2.4.0+)
eda-cli build --config ./eda.config.json

// ❌ FAILS IN v2.4.0 (Unrecognized key)
{
  "project_name": "soc_top",
  "legacy_pdk_path": "/opt/pdk/v1" 
}

// ✅ COMPLIANT SCHEMA (v2.4.0)
{
  "project_name": "soc_top",
  "pdk_settings": {
    "root_path": "/opt/pdk/v1"
  }
}
eda-cli build --target synthesis --multi-die ./die_map.json
# Upgrade via enterprise package manager
pip install eda-cli-tools --upgrade

# Verify installed version
eda-cli --version
