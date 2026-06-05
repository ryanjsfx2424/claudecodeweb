
## Cloud Credentials

- **Provider:** GCP
- **Project:** adktest-490619
- **Service account:** claude-agent@adktest-490619.iam.gserviceaccount.com

### Roles granted

| Role | Reason |
|------|--------|
| `roles/bigquery.dataEditor` | Write/update tables in the project's BigQuery dataset |
| `roles/bigquery.jobUser` | Run queries (read Citibike public data, cross-project reads, write results) |
| `roles/storage.objectAdmin` | Stage Citibike source files and serve website static assets from GCS |
| `roles/run.developer` | Deploy and manage the Cloud Run web service for visualizations |

### Cross-project access (action required)

Reading `nyu-datasets.weather.m_weather_daily_nyc` requires the **nyu-datasets project admin** to grant this service account `roles/bigquery.dataViewer` on that dataset. Request this separately — it cannot be done from this project.

**In the meantime**, a synthetic stand-in dataset has been created at `adktest-490619.synthetic_weather.m_weather_daily_nyc` with the same schema (`date`, `tmax_f`, `tmin_f`, `prcp_mm`, `snow_mm`, `snwd_mm`). Use this table for local development and testing until cross-project access is granted. Update queries from `nyu-datasets.weather.m_weather_daily_nyc` → `adktest-490619.synthetic_weather.m_weather_daily_nyc`.

### Authentication

This is a multi-user setup. Each team member has their own encrypted credentials file: `.cloud-credentials.<email>.enc`. The agent authenticates automatically at session start via `.claude/hooks/cloud-auth.sh`.

To authenticate manually in a session, say: "authenticate to GCP".

### Adding a team member

Say: "add me to cloud access" — the agent will run the Add Team Member workflow. The new team member needs their own `GCP_CREDENTIALS_KEY` or `CLOUD_CREDENTIALS_KEY` environment variable set in Claude Code on the Web.

### Escalating permissions

If a GCP command fails with 403 / access denied, say: "I got a permission error" and the agent will identify the required role and guide you through granting it.
