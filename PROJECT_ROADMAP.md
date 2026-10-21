# FundiLinksProject: Week 1–7 Roadmap

This file organizes the current project into seven review stages. It is a working roadmap inferred from the current codebase, not a substitute for the official course brief. Once the weekly instructions are available, map each exact deliverable to the appropriate stage and update the status honestly.

## Week 1 — Problem and project foundation
- Define the problem: informal, unreliable sourcing of short-term skilled labour.
- Identify the two main user roles: worker and employer.
- State the project goal, scope, assumptions, and expected value.
- Reference: `README.md`, `TEAM_CHARTER.md`.

## Week 2 — Requirements and initial interface
- Document the key user journeys and functional requirements.
- Establish the initial HTML/CSS structure and shared visual styling.
- Review homepage and navigation.
- Main files: `src/index.html`, `src/index.css`, `src/main.js`.

## Week 3 — Authentication and role-based journeys
- Review registration and login for worker/employer roles.
- Verify that navigation and redirects match the selected role.
- Main files: `src/login.html`, `src/login.css`, `src/login.js`, `src/main.js`.

## Week 4 — Job discovery and employer workflows
- Review job listing, category filtering, and application interaction.
- Review employer dashboard and job-posting form.
- Main files: `src/jobs.html`, `src/jobs.css`, `src/jobs.jsx`, `src/dashboard.html`, `src/dashboard.js`, `src/post-job.html`.

## Week 5 — Integration and review
- Check that pages agree on data shapes, endpoint paths, and user roles.
- Review the JSON demo data and identify incomplete or inconsistent behaviour.
- Main files: `src/db.json`, `API_NEEDS.md`, `CONTRACT_QUESTIONS.md`, `ENDPOINT_LIST.md`.

## Week 6 — API and contract work
- Review the Express API and compatibility routes.
- Keep the OpenAPI contract aligned with actual request/response behaviour.
- Main files: `app.js`, `routes.js`, `openapi.yaml`, `CONTRACT_DEVIATIONS.md`.

## Week 7 — Testing, bug fixes, and handover
- Run automated tests and fix failures based on observed results.
- Run a partner test exchange if required by the course; record actual pass/fail evidence.
- Review CI workflow and final run instructions.
- Main files: `__tests__/api.test.js`, `.github/workflows/api-tests.yml`, `PARTNER_TEST_RESULTS.md`, `README.md`.

## Verification checklist

- [ ] Official Week 1–7 instructions checked against this roadmap.
- [ ] Install dependencies with `npm install`.
- [ ] Run `npm test` and record the actual result.
- [ ] Start the API and browse the web app locally.
- [ ] Check worker and employer flows end to end.
- [ ] Check API responses against `openapi.yaml`.
- [ ] Complete partner testing only if it was actually performed.
- [ ] Record known limitations and final evidence.

## Known caveat

This codebase is a learning/demo app using a JSON-file data store and localStorage-based demo authentication. It is not suitable for real user data without substantial security and persistence improvements.
