# UCE Day Hospital

UCE Day Hospital is an academic web engineering project at Universidad Central del Ecuador (UCE). The project proposes a healthcare appointment management system for the university's Day Hospital. Its goal is to give patients a single place to check availability and manage appointments while helping healthcare professionals and administrators coordinate schedules and services.

## Project Status

The project is in the analysis and design phase. The repository contains the initial monorepo structure. Application implementation, local setup instructions, and deployment workflows are planned for subsequent development work.

## Planned Features

| User | Capabilities |
| --- | --- |
| Visitor | Browse institutional information, healthcare services, announcements, and operating hours. |
| Patient | Register and sign in, browse available time slots, book appointments, view appointment history, and cancel or reschedule eligible appointments. |
| Healthcare Professional | View an assigned agenda and record patient attendance or absence. |
| Administrator | Manage healthcare units, professionals, working schedules, and closures. Review appointments, record administrative cancellations, and view audit records and aggregate reports. |

The system also plans email confirmations and reminders, simulated payments through Stripe Sandbox, and an AI-assisted search feature for approved institutional information. The AI feature is limited to institutional questions such as service availability and operating hours. Clinical records, diagnosis, prescriptions, telemedicine, and real payments are outside the MVP scope.

## Appointment Rules

- Appointments use 15-minute time slots. Patients select an available healthcare professional when booking.
- The proposed booking window opens 24 hours before the appointment and closes one hour before it starts.
- Patients can cancel eligible appointments or reschedule confirmed appointments up to 30 minutes before the scheduled start.
- The backend will prevent overlapping active appointments for both patients and professionals. If a rescheduling attempt fails, the original booking remains in place.
- Operating hours and patient booking limits are MVP assumptions pending hospital validation.

## Planned Architecture and Technology Stack

| Area | Technologies and purpose |
| --- | --- |
| Public portal | **Astro** and **Contentful** for publishing institutional information and service announcements. **Render** is the proposed hosting platform for the portal. |
| Web application | **React**, **TypeScript**, **Vite**, and **Material UI** for the authenticated application. **Module Federation** is planned for loading the administrative microfrontend, with **WebAssembly** for selected reporting calculations. |
| Backend | **Java 21** and **Spring Boot** in a modular monolith. **REST** supports application operations, **GraphQL** supports selected queries, and **webhooks** handle integration events. **OpenAPI** documents the REST contract. |
| Identity and access | **Keycloak** and **OpenID Connect** for authentication. The backend will enforce permissions by role and resource ownership. |
| Data | **PostgreSQL** for transactional data such as appointments, **MongoDB** for audit records, **Redis** for catalog caching, and **Qdrant** for institutional semantic search. |
| Automation and payments | **n8n** for notification workflows, **Resend** for transactional email, and **Stripe Sandbox** for simulated payments. |
| Institutional search | **Retrieval-Augmented Generation (RAG)** with embeddings and Qdrant. The search feature will retrieve relevant institutional sources before generating an answer. |
| Infrastructure and delivery | **Docker Compose** for local development, **GitHub Actions** for CI/CD, and **Docker Hub** for container images. The proposed deployment uses **AWS** for application hosting, API routing, and storage, with **Cloudflare** for DNS and perimeter protection. |
| Quality and monitoring | **JUnit**, **Vitest**, **Testcontainers**, **Playwright**, and **k6** for planned testing. **CloudWatch**, **Sentry**, and **Site24x7** support planned monitoring and alerting. |

The project plans separate local, QA, and production demonstration environments. Testing and demonstrations will use synthetic patient data. Credentials will be managed separately from the source code.

## Repository Structure

| Path | Purpose |
| --- | --- |
| `backend/` | Spring Boot application, business rules, and API endpoints |
| `frontend-public/` | Astro public portal |
| `frontend-app/` | React host application for authenticated users |
| `frontend-admin/` | Administrative microfrontend |
| `packages/ui/` | Shared interface components |
| `packages/api/` | Shared API contracts and client code |
| `infra/docker/` | Container definitions and local environment setup |
| `infra/aws/` | AWS infrastructure configuration |
| `infra/keycloak/` | Identity provider configuration |
| `infra/n8n/` | Automation workflow definitions |
| `tests/e2e/` | End-to-end tests |
| `tests/load/` | Performance and load tests |
| `.github/workflows/` | GitHub Actions workflows |

## Project Roadmap

| Phase | Objective |
| --- | --- |
| Sprint 0 | Define the MVP scope, team responsibilities, and documentation baseline. |
| Sprint 1 | Review requirements, business rules, architecture, and user flows, and prepare evidence for the initial presentation. |
| Sprint 2 | Begin implementation with the monorepo, local environment, application structure, CI, and authentication. |
| Later increments | Implement the catalog and appointment flows, administrative features, notifications, sandbox payments, institutional search, and reporting. |

## Documentation and Project Tracking

System requirements, business rules, architecture diagrams, and acceptance criteria are maintained in Confluence. Epics, stories, tasks, and subtasks are tracked in Jira under project key `DP`.

- [Confluence project documentation](https://uce-day-hospital2026-t86ks6d9.atlassian.net/wiki/spaces/UDH1/overview)
- [Jira project backlog](https://uce-day-hospital2026-t86ks6d9.atlassian.net/jira/software/projects/DP/boards/1/backlog)