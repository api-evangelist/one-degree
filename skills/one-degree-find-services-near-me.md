---
name: Find social services near a location
description: Search One Degree for community-service opportunities near a location and retrieve their details, schedule, and access instructions.
api: openapi/one-degree-openapi.yml
operations: [listOpportunities, getOpportunity, getOpportunitySchedule, getOpportunityAccessInstructions]
---

# Find social services near a location

Use the One Degree Resource Server API to help someone find local social-service programs (food, shelter, health, employment, etc.).

## Auth
- Every request needs an `api_key` query parameter. Request one at http://socialservicedata.org/api/get-key/.
- These are all read (`GET`) operations, so no request signature is needed.

## Steps
1. **Search** with `listOpportunities` on `GET /opportunities`. Pass geo and text query params: `query[text]` (e.g. `health clinic`), `query[lat]`, `query[long]`, `query[distance]` (km radius), and optionally `query[tags]`. Use `page`/`per_page` to paginate. Results are scored by best match and distance.
2. For a promising result, call `getOpportunity` (`GET /opportunities/{opportunity_id}`) to load full details.
3. Call `getOpportunitySchedule` (`GET /organizations/{organization_id}/opportunities/{opportunity_id}/schedule`) for hours.
4. Call `getOpportunityAccessInstructions` (`GET /organizations/{organization_id}/opportunities/{opportunity_id}/access_instructions`) for how to access the service.

## Conventions & errors
- Default response is JSON; append `.xml` to an endpoint for XML.
- Errors return `{ "status": "error", "error": "<message>" }`; a missing key yields `400 Missing API key.` (see errors/one-degree-problem-types.yml).
- Timestamps are ISO 8601 UTC. Data is licensed CC BY-NC 4.0 — attribute One Degree and do not use commercially.
