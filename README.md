# E2E QA Automation Project

Automated end-to-end testing framework built with **Playwright**, covering Smoke, Functional, and Regression test suites across **Chromium, Firefox, and WebKit**. Fully containerized with **Docker** and integrated with **GitHub Actions CI/CD**, automatically deploying a live HTML test report on every push.

---

## Live Test Report

**[View Latest Test Report →](https://bushra123445.github.io/Testing-E2E-Qa-Automation/)**

The report updates automatically after every push to `main`, showing pass/fail status, execution time, screenshots, videos, and traces for every test across all three browsers.

---

## Tech Stack

| Category            | Tools Used                          |
|----------------------|--------------------------------------|
| Test Framework        | Playwright (TypeScript)             |
| Browsers Covered      | Chromium, Firefox, WebKit           |
| Reporting             | Playwright HTML Reporter, Allure    |
| Containerization      | Docker                              |
| CI/CD                 | GitHub Actions                      |
| Report Hosting        | GitHub Pages                        |
| Local Server          | http-server                         |

---

## Test Suites

| Suite       | Location                        | Purpose                                              |
|-------------|----------------------------------|-------------------------------------------------------|
| Smoke       | `test/smoke/`                   | Quick checks on critical user journeys                |
| Functional  | `test/functional/`              | Detailed feature-level flows (Login → Dashboard etc.) |
| Regression  | `test/regression/`              | Full end-to-end user journey validation               |

All suites run against **Chromium, Firefox, and WebKit** on every execution.

---

## Project Structure

```
E2E-Qa-Automation/
├── test/
│   ├── smoke/
│   ├── functional/
│   └── regression/
├── performance/
│   └── load-test.js          # K6 load testing script
├── .github/
│   └── workflows/
│       └── playwright.yml    # CI/CD pipeline (build, test, deploy)
├── playwright-report/        # Auto-generated HTML report (gitignored)
├── allure-results/           # Auto-generated Allure results (gitignored)
├── Dockerfile
├── playwright.config.ts
├── package.json
└── README.md
```

---

## Running Tests Locally

### Prerequisites
- Node.js (v20+)
- Docker Desktop (optional, for containerized runs)

### Install dependencies
```bash
npm ci
npx playwright install --with-deps
```

### Run all tests (all browsers)
```bash
npx playwright test
```

### Run a specific suite
```bash
npx playwright test test/smoke
```

### Run on a specific browser only
```bash
npx playwright test --project=chromium
```

### View the HTML report after a local run
```bash
npx playwright show-report
```

---

## Running Tests via Docker

### Build the image
```bash
docker build -t e2e-qa-automation .
```

### Run the container
```bash
docker run --rm e2e-qa-automation
```

---

## CI/CD Pipeline (GitHub Actions)

On every push to `main`, the workflow (`.github/workflows/playwright.yml`) automatically:

1. **Build** — Builds the Docker image to validate the containerized setup.
2. **Test** — Installs dependencies and browsers, then runs the full test suite across Chromium, Firefox, and WebKit.
3. **Deploy** — Publishes the generated HTML report to GitHub Pages, producing a live, shareable report URL.

Check the **Actions** tab in this repository to see the status of the latest run.

---

## Performance Testing (K6)

A load test script is included at `performance/load-test.js`, simulating up to 450 concurrent virtual users. Run it locally with:

```bash
k6 run performance/load-test.js
```

---

## Notes

- `.env`, `node_modules/`, `playwright-report/`, and `test-results/` are excluded from version control via `.gitignore`.
- Test data and reusable helper functions are organized under `test-data/` and `utils/` respectively.
