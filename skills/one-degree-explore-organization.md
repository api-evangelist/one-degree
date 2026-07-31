---
name: Explore a provider organization and its locations
description: Look up a One Degree organization, list the opportunities it offers, and get its locations, phones, and schedules.
api: openapi/one-degree-openapi.yml
operations: [getOrganization, getOrganizationLocations, getLocationPhones, getLocationSchedule]
---

# Explore a provider organization and its locations

Use the One Degree Resource Server API to profile a social-service organization and its physical locations.

## Auth
- Every request needs an `api_key` query parameter. Request one at http://socialservicedata.org/api/get-key/.
- All read (`GET`) operations — no request signature needed.

## Steps
1. Call `getOrganization` (`GET /organizations/{organization_id}`) to load the organization (id can be a slug, e.g. `compass-family-services`).
2. Call `getOrganizationLocations` (`GET /organizations/{organization_id}/locations`) to list its physical locations.
3. For a location, call `getLocationPhones` (`GET /organizations/{organization_id}/locations/{location_id}/phones`) for contact numbers.
4. Call `getLocationSchedule` (`GET /organizations/{organization_id}/locations/{location_id}/schedule`) for hours of operation.

## Conventions & errors
- Collections support `page`, `per_page`, and `titles_only` pagination.
- Default response is JSON; append `.xml` for XML.
- Errors use the `{ "status": "error", "error": "<message>" }` envelope (see errors/one-degree-problem-types.yml).
- Data is licensed CC BY-NC 4.0.
