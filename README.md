# Azure Monitoring & Alerting Lab

This project demonstrates hands-on experience with Azure Monitor, custom alerts, and automated VM deployments via ARM templates.

## Tools & Services Used

- Azure Resource Manager (ARM)
- Azure Monitor
- VM Insights
- Action Groups
- Kusto Query Language (KQL)
- Azure Alerts & Suppression Rules

## Lab Tasks Completed

1. **Deploy a VM with ARM Template**  
   Deployed a Linux VM via `az104-11-vm-template.json` with associated network infrastructure.

2. **Enable Azure Monitor Insights**  
   Enabled VM Insights and verified agent installation.

3. **Configure Alerts & Actions**  
   Created an alert rule for VM deletion and linked an email action group.

4. **Simulate Alert Event**  
   Deleted VM to trigger the alert and verified email delivery from `azure-noreply@microsoft.com`.

5. **Suppress Alerts During Maintenance**  
   Created an alert processing rule to suppress alerts between 10 PM–7 AM (local time).

6. **Run KQL Log Queries**  
   Queried heartbeat metrics and resource utilization using Azure Monitor Logs.

## KQL Query

```kql
InsightsMetrics
| where TimeGenerated > ago(1h)
| where Name == "UtilizationPercentage"
| summarize avg(Val) by bin(TimeGenerated, 5m), Computer
| render timechart
