# FundiLinksProject

FundiLinks is a web application concept for connecting Kenyan employers who need short-term skilled work with nearby workers ("fundis"). This repository is a separate consolidated working copy of the original FundiLinks project, with the Week 6–7 API and testing work included for continued development.

## Current features

- Worker and employer registration/login demo
- Role-aware navigation and redirects
- Browse and filter active job listings
- Submit job applications and track/cancel pending applications
- Employer dashboard and job-posting form
- Express API, JSON-file demo data, and OpenAPI contract
- Jest/Supertest API tests and GitHub Actions test workflow

## Technology

- HTML, CSS and JavaScript
- React via CDN/Babel for the jobs page
- Node.js and Express
- JSON file data store at `src/db.json`
- Jest and Supertest
- OpenAPI 3 specification in `openapi.yaml`

## Run locally

Prerequisite: install a current Node.js LTS version.

1. Clone this repository:
   ```bash
   git clone https://github.com/AringoA/FundiLinksProject.git
   cd FundiLinksProject
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start the API in one terminal:
   ```bash
   npm start
   ```
4. Start the static website in another terminal:
   ```bash
   npm run serve:web
   ```
5. Open `http://localhost:8080/src/index.html`.

The API listens on port 3001 by default. See `package.json` and `openapi.yaml` for available scripts and endpoint contracts.

## Testing

Run the automated tests with:

```bash
npm test
```

Tests should be run locally and through GitHub Actions before treating the project as verified. Do not report partner testing as complete until the exchange has actually taken place; record real results in `PARTNER_TEST_RESULTS.md`.

## Week-by-week project organization

See [PROJECT_ROADMAP.md](PROJECT_ROADMAP.md). The week labels are a working organization aid, not a claim that every course requirement has been met. Match them against the official weekly guidelines and deliverables.

## Important demo security note

This is a student/demo application. The JSON-file database and browser localStorage authentication are not production-grade. The mock database may store passwords in plaintext. Use password hashing, secure server-side sessions or tokens, authorization checks, input validation, and a real database before any real deployment. Do not use real passwords or personal information in the demo.

## Reference repository

The original project remains separate: [AringoA/FundiLinks](https://github.com/AringoA/FundiLinks). This repository is intended to be the clean consolidated version for review and comparison.
