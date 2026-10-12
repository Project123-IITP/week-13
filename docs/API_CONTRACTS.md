# Proposed API Contracts — `/api/v1`

Planning examples only. No endpoint is implemented by this document. Use fictional data in tests and demos.

## Common response conventions

Success responses return JSON. Errors should use a consistent shape:

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "The request contains invalid fields.",
    "details": [{ "field": "startAt", "message": "Must be a valid date-time." }]
  }
}
```

Common status codes: `200` success, `201` created, `400` invalid request, `401` unauthenticated, `403` unauthorized, `404` not found, `409` conflict, `422` business-rule validation failure, `500` unexpected server error.

## Authentication

### `POST /auth/login`
Request:
```json
{ "email": "staff@example.test", "password": "example-only" }
```
Success (planned): `200`, returns a safe user summary and establishes the chosen session/token mechanism. Never return a password or password hash.

Validation: valid email format; non-empty password. Invalid credentials return a generic `401` response.

### `POST /auth/logout`
Purpose: invalidate the active session/token according to the chosen auth strategy. Planned success: `204`.

### `GET /auth/me`
Purpose: return the current authenticated user's safe profile. Requires authentication.

## Dashboard

### `GET /dashboard/summary`
Query parameters: optional `date=YYYY-MM-DD`.

Example response:
```json
{
  "date": "2026-10-12",
  "summary": {
    "totalAppointments": 24,
    "completed": 8,
    "pending": 6,
    "cancelled": 2
  }
}
```
Counts are fictional examples. Define whether counts are clinic-wide or user-scoped before implementation.

## Appointments

### `GET /appointments`
Query parameters:
- `date` optional `YYYY-MM-DD`
- `status` optional enum: `scheduled`, `confirmed`, `completed`, `cancelled`, `no_show`
- `search` optional short string
- `page` positive integer, default `1`
- `limit` bounded integer, default `10`, maximum `100`

Example response:
```json
{
  "items": [
    {
      "id": "appt_demo_001",
      "patientId": "patient_demo_001",
      "providerId": "user_demo_001",
      "startAt": "2026-10-12T09:30:00+05:30",
      "endAt": "2026-10-12T10:00:00+05:30",
      "status": "confirmed",
      "reason": "Routine review"
    }
  ],
  "pagination": { "page": 1, "limit": 10, "total": 1, "totalPages": 1 }
}
```

### `GET /appointments/:id`
Purpose: return appointment details plus only the patient/provider fields needed by the current role. Requires authorization.

### `POST /appointments`
Request:
```json
{
  "patientId": "patient_demo_001",
  "providerId": "user_demo_001",
  "startAt": "2026-10-12T09:30:00+05:30",
  "endAt": "2026-10-12T10:00:00+05:30",
  "reason": "Routine review"
}
```
Expected: `201` with created appointment. Validate referenced records, valid date order, allowed status defaults, and scheduling conflicts. Do not trust client-supplied provider permissions.

### `PATCH /appointments/:id`
Allow only explicitly supported fields, for example `startAt`, `endAt`, `reason`, and `status`. Validate status transitions and authorization. Return `200` with updated record or `404` if not found.

## Patients

### `GET /patients`
Query parameters: `search`, `page`, `limit`. Search should be bounded and restricted to authorized fields. Return paginated results with minimum necessary information.

### `GET /patients/:id`
Purpose: return the patient profile fields required for the workflow. Requires record-level authorization.

### `POST /patients`
Staff-only planned endpoint. Validate required fields, normalize email/phone where applicable, and avoid collecting unnecessary sensitive information. Return `201`.

### `PATCH /patients/:id`
Staff-only planned endpoint. Validate allowed fields and record-level authorization. Return `200`.

## API decisions still required

- Session cookie versus token strategy.
- Exact role and permission matrix.
- Appointment conflict policy and allowed status transitions.
- Timezone storage/display rules.
- Which patient fields are essential for each screen.
- Whether patient self-service is in scope for P0 or P1.
