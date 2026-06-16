# NOAVIA — Technical Troubleshooting Guide

## My AI Agent Is Not Responding
1. Check if the agent service is running by visiting your agent dashboard at https://portal.noavia.de/agents
2. If the status shows "Offline," try restarting the agent from the dashboard (click Restart)
3. If using an on-premise deployment, verify that Docker containers are running: `docker ps` should list the NOAVIA agent containers
4. Check your internet connection and firewall rules — the agent requires outbound HTTPS access on port 443
5. If the issue persists, contact support@noavia.de with your Kundennummer and agent ID

## Webhook Is Not Receiving Data
1. Verify the webhook URL is correctly configured in your source system
2. Ensure the webhook endpoint is accessible (test with a simple POST request using curl or Postman)
3. Check that the payload format matches the expected schema (JSON with required fields)
4. Review the n8n execution log at https://portal.noavia.de/workflows for error details
5. If your company uses a corporate firewall or proxy, ensure the NOAVIA webhook domain is whitelisted

## AI Responses Are Inaccurate or Irrelevant
1. Check if the knowledge base is up to date — outdated documents lead to outdated answers
2. Review the RAG retrieval logs to see which documents are being retrieved
3. The AI may need retraining or prompt adjustment if your business processes have changed
4. Contact your NOAVIA account manager to schedule a knowledge base refresh
5. For critical accuracy issues, submit a ticket with category "AI Quality" and include example queries with expected vs. actual responses

## Integration Issues with ERP / External Systems
1. Verify API credentials have not expired — most API keys rotate every 90 days
2. Check the API rate limits for your plan (Standard: 1,000 req/hour, Enterprise: unlimited)
3. Review the integration log at https://portal.noavia.de/integrations
4. For SAP or DATEV integrations, ensure the middleware connector version is current
5. Contact support with the integration name, error message, and timestamp

## Performance Is Slow
1. Check the NOAVIA status page at https://status.noavia.de for any ongoing incidents
2. For on-premise deployments, verify that the server meets minimum requirements: 8 GB RAM, 4 CPU cores, 50 GB SSD
3. Large document processing jobs (>100 documents) may queue during peak hours — check the job queue in your dashboard
4. If using vector search, the Qdrant instance may need more memory — contact support to review your configuration

## How to Access Logs
All execution logs are available in the client portal:
1. Go to https://portal.noavia.de
2. Navigate to Workflows → Execution History
3. Filter by date, status (success/error), or workflow name
4. Click on any execution to see detailed step-by-step logs
Logs are retained for 30 days. For longer retention, enable log export to your own storage.
