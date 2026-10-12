# Product Requirements Document — VitalSync

## 1. Product summary

VitalSync is a responsive healthcare appointment and patient-management dashboard concept for clinic staff and patients. It centralizes appointment overview, appointment details, and patient details in a consistent UI.

## 2. Users

- **Clinic staff:** review the day's workload, search appointments, create or update appointments, and view patient records.
- **Patient:** review their own upcoming appointments and relevant appointment details.
- **Administrator (future/limited scope):** manage access and review operational activity.

## 3. Problem

Appointment and patient workflows can become difficult to scan when information is spread across screens or displayed without clear status and responsive behavior. VitalSync aims to reduce navigation friction and make the current appointment state easy to understand.

## 4. Goals and metrics

- A user can locate an appointment using search/filter controls.
- A user can open an appointment and identify its date, time, status, and linked patient.
- Authorized staff can create and update appointments.
- Important workflows remain usable at desktop, tablet, and mobile widths.
- Every data-driven view defines loading, empty, error, and success states.

Possible evaluation metrics for a later implementation:
- Task completion rate for finding an appointment.
- Number of steps to open a patient from an appointment.
- Responsive QA pass rate across agreed viewport sizes.
- Form validation and API error handling test coverage.

## 5. Non-goals

- Diagnosis, treatment recommendations, or clinical decision support.
- Billing, insurance claims, e-prescriptions, or telemedicine.
- Real patient data in public development environments.
- A claim of HIPAA, GDPR, or other compliance without a formal review.
- Functional code implementation during Sprint 13.

## 6. User stories

### P0
- As clinic staff, I want a dashboard summary so I can understand today's workload.
- As clinic staff, I want to list and filter appointments so I can find the correct booking.
- As clinic staff, I want to view appointment details so I can verify time, status, and patient association.
- As clinic staff, I want to create and update appointments so the schedule can be maintained.
- As an authorized user, I want to view patient details needed for the workflow.
- As a user, I want the layout to work on desktop, tablet, and mobile.
- As a user, I want clear loading, empty, error, and validation feedback.

### P1
- As clinic staff, I want to search patients by a limited set of fields.
- As a patient, I want to review my own appointments.
- As clinic staff, I want pagination and date filters for larger lists.

### P2
- As clinic staff, I want a calendar view and reminders.
- As an administrator, I want an audit history for important record changes.

## 7. Functional requirements

1. Authentication screens must define invalid credentials, pending, success, and failure states.
2. Protected screens must require an authenticated session in the implemented system.
3. Dashboard cards must be derived from the dashboard API response, not hard-coded production data.
4. Appointment list must support status/date filtering and pagination.
5. Appointment detail must display a linked patient and appointment metadata.
6. Appointment creation/update must validate required fields on both client and server.
7. Patient views must expose only the fields required by the user's role and task.
8. Mutations must refresh or invalidate relevant server-state queries.
9. Mobile layout must avoid horizontal overflow and provide usable touch targets.
10. Destructive or status-changing actions must provide confirmation where appropriate.

## 8. Non-functional requirements

- Responsive at the agreed desktop, tablet, and mobile viewports.
- Keyboard-accessible forms, focus states, labels, and dialogs.
- Server-side input validation and authorization.
- No secrets or real patient information committed to Git.
- Consistent API error format and useful user-facing error messages.
- Future implementation should include linting, type-checking, automated tests, and production build validation.

## 9. Acceptance criteria

- Each P0 screen has an approved Figma layout for desktop, tablet, and mobile.
- A reviewer can navigate the Figma file and identify the intended screen variants.
- The state tree distinguishes server data from client-only UI state.
- Each proposed endpoint has documented inputs, output shape, validation, and error cases.
- The ERD uses 3–5 collections and defines references and indexes.
- The README links to all planning artifacts.
- The demo video is no longer than three minutes and does not represent designs as implemented functionality.
