
## Cloud Credentials

- **Provider:** GCP
- **Project:** adktest-490619
- **Service account:** claude-agent@adktest-490619.iam.gserviceaccount.com

### Roles granted

| Role | Reason |
|------|--------|
| `roles/bigquery.dataEditor` | Read/write data in BigQuery datasets and tables |
| `roles/bigquery.jobUser` | Run queries and jobs against the project |
| `roles/storage.objectAdmin` | Read/write GCS buckets and objects |

### Authentication

This is a multi-user setup. Each team member has their own encrypted credentials file: `.cloud-credentials.<email>.enc`. The agent authenticates automatically at session start via `.claude/hooks/cloud-auth.sh`.

To authenticate manually in a session, say: "authenticate to GCP".

### Adding a team member

Say: "add me to cloud access" — the agent will run the Add Team Member workflow. The new team member needs their own `GCP_CREDENTIALS_KEY` or `CLOUD_CREDENTIALS_KEY` environment variable set in Claude Code on the Web.

### Escalating permissions

If a GCP command fails with 403 / access denied, say: "I got a permission error" and the agent will identify the required role and guide you through granting it.
