# Troubleshooting & Error Resolution: `eda-cli` Build Failures

This guide details common execution failures, environment misconfigurations, and timing closure issues encountered during synthesis and static timing analysis runs with `eda-cli`, along with resolution steps.

---

## Diagnostic Quick Matrix

| Error Code | Error Type | Primary Cause | Immediate Resolution |
| :--- | :--- | :--- | :--- |
| **`ERR_LIC_01`** | License Server Failure | FlexLM daemon unreachable or port blocked. | Verify `EDA_LICENSE_FILE` environment variable and test port connectivity. |
| **`ERR_PDK_04`** | Target Library Missing | Invalid or unreadable `.lib` path in `eda.config.json`. | Check file permissions and path syntax under `PDK_ROOT`. |
| **`ERR_TIM_127`** | Negative Slack Violation | Critical path setup time violation exceeds threshold. | Review timing report (`.rpt`) and adjust pipeline registers or clock period. |

---

## Error Details & Resolution Procedures

### Error `ERR_LIC_01`: License Server Connection Timeout

#### Problem Statement
The build process terminates during elaboration with the following console output:

```text
[ERROR] Failed to check out license feature 'synthesis_engine_v2'.
[ERROR] FlexLM error code: -15,570. System error: 111 (Connection refused).
[FATAL] Exiting with status code 2.

echo $EDA_LICENSE_FILE
# Output should match: 27000@lic-server.internal.net

nc -zv lic-server.internal.net 27000

[INFO] Technology mapping complete.
[WARN] Critical path slack is negative: -0.420 ns.
[ERROR] Build failed due to setup timing violations.
[FATAL] Exiting with status code 127.

cat ./dist/reports/timing_summary.rpt
{
  "synthesis_options": {
    "allow_lvt_cells": true,
    "effort_level": "high"
  }
}
