# REST API Reference: Cloud Job Execution & Workspace Service

The Cloud Job Execution API allows developers to programmatically manage remote synthesis workflows, query job execution statuses, and download generated artifacts over HTTP/HTTPS.

---

## Base URL & Environment

All API requests must be directed to the following base endpoint:

```text
[https://api.cloud-eda.internal.net/v1](https://api.cloud-eda.internal.net/v1)
Authorization: Bearer <YOUR_API_SERVICE_TOKEN>

curl -X POST "[https://api.cloud-eda.internal.net/v1/jobs/synthesis](https://api.cloud-eda.internal.net/v1/jobs/synthesis)" \
     -H "Authorization: Bearer eda_tok_89f2a7b1c4e" \
     -H "Content-Type: application/json" \
     -d '{
           "project_name": "soc_core_v2",
           "top_module": "alu_top",
           "target_freq_mhz": 500.0,
           "thread_count": 8
         }'
{
  "status": "success",
  "data": {
    "job_id": "job_99842_a",
    "project_name": "soc_core_v2",
    "state": "QUEUED",
    "estimated_duration_sec": 45,
    "created_at": "2026-08-02T10:15:30Z"
  }
}

curl -X GET "[https://api.cloud-eda.internal.net/v1/jobs/job_99842_a](https://api.cloud-eda.internal.net/v1/jobs/job_99842_a)" \
     -H "Authorization: Bearer eda_tok_89f2a7b1c4e"
{
  "status": "success",
  "data": {
    "job_id": "job_99842_a",
    "state": "COMPLETED",
    "execution_time_sec": 38.4,
    "metrics": {
      "gate_count": 14205,
      "worst_negative_slack_ns": 0.012,
      "total_power_mw": 3.42
    },
    "artifacts_url": "[https://api.cloud-eda.internal.net/v1/jobs/job_99842_a/artifacts](https://api.cloud-eda.internal.net/v1/jobs/job_99842_a/artifacts)"
  }
}

{
  "status": "success",
  "message": "Job job_99842_a has been successfully cancelled."
}
