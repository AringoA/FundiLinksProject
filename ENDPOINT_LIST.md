# ENDPOINT_LIST.md — FundiLink (Team 15)

## Downstream endpoints — FundiLink provides to SettleIn

| # | Method | Endpoint | Purpose | Maps to Need |
|---|--------|----------|---------|---------------|
| 1 | GET | `/api/jobs?status=active` | Returns active job/service listings; empty array when none match | Statement 1 |
| 2 | GET | `/api/jobs?county={county}&category={category}&status=active` | Filters active listings by location and category near a student's accommodation | Statement 2 |
| 3 | GET | `/api/jobs/{jobId}` | Returns one job's details, including status and pay | Statements 3, 4 |
| 4 | GET | `/api/jobs/{jobId}/status` | Returns the current availability status without the full job payload | Statement 3 |
| 5 | GET | `/api/applications/{applicationId}/status` | Returns the current application status | Statement 5 |
| 6 | GET | `/api/applications/{applicationId}/subscribe` | Sends one initial status event as Server-Sent Events (SSE), then closes the connection. This is a snapshot, not a persistent push subscription. | Statement 5 |
| 7 | POST | `/api/applications` | Creates a new application/service request | Statement 6 |
| 8 | PUT | `/api/applications/{applicationId}` | Updates an existing pending application (e.g. reschedule or edit details) | Statement 7 |
| 9 | DELETE | `/api/applications/{applicationId}` | Cancels a pending application; success returns 204 with no body | Statement 8 |

## Contract caveat

The current implementation of `/api/applications/{applicationId}/subscribe` sends only the initial status snapshot and ends the response. It does not push later status changes. If SettleIn needs live updates, agree a persistent SSE design with the consumer and implement/test it before claiming real-time subscriptions.
