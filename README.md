# Slack Notifier GitHub Action

This GitHub Action sends a Slack notification on build success.

## Usage

Follow these steps to integrate the Slack Notifier into your GitHub Actions workflow:

### 1. Create a GitHub Action Workflow

Add the following `.github/workflows/slack-notifier.yml` file to your repository. This file configures the GitHub Action to trigger a Slack notification on build success.

```yaml
name: Slack Notifier

on:
  workflow_dispatch:

jobs:
  slack-notifier:
    runs-on: ubuntu-latest
    steps:
      - name: Send Slack Notification
        run: |
          curl -X POST -H 'Content-type: application/json' --data '{"text": "✅ *Build Succeeded*\\nRepository: ${{ github.repository }}\\nBranch: ${{ github.ref_name }}\\nCommit: ${{ github.sha }}\\nWorkflow: ${{ github.workflow }}\\nJob: ${{ github.job }}\\n🔗 [View Logs](${{ github.server_url }}/${{ github.repository }}/actions/runs/${{ github.run_id }})"}' ${{ secrets.SLACK_WEBHOOK_URL }}
