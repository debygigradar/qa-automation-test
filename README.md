# 🧪 QA Automation Assessment (Playwright + TypeScript)

Hi 👋  

Thank you for your interest in joining our team as a **QA Automation Engineer**.  
This short practical test is designed to evaluate your hands-on skills with **Playwright**, focusing on test design, stability, and code quality.

Please read carefully and submit your work following the instructions below.

---

## 🎯 Objective
Create a small **end-to-end UI test suite** using **Playwright (TypeScript)** that verifies key functionality on Upwork’s public job search pages.  
No login or form submission is required — only public, read-only interactions.

---

## ⚙️ Requirements
- Use **TypeScript** and **Playwright Test** runner.
- Organize your code with **Page Objects** and reusable fixtures.
- Use **semantic, stable selectors** (no brittle CSS paths).
- Generate useful **artifacts** (screenshots, traces, reports).
- Keep everything self-contained — no external paid dependencies.

**Target site:** [https://www.upwork.com/nx/search/jobs/](https://www.upwork.com/nx/search/jobs/)

---

## 🧠 Tasks

### **Task A — Functional Flow**
1. Open Upwork job search page
2. Search for **“qa automation”**.  
3. Apply one visible filter (e.g., experience level).  
4. Verify that job cards are displayed (non-zero results).  
5. Open the **first job** in a new tab.  
6. Validate the following on the job detail page:
   - Job title is visible  
   - Description is non-empty  
   - Client Metadata exists  
7. Save a full-page screenshot to `artifacts/job-detail.png`.

---

### **Task B — Pagination & Result Integrity**
1. Collect the first 5 job titles and URLs from **page 1**.  
2. Go to the **next page**.  
3. Assert that at least one job is different from page 1.  
4. Save both sets to `artifacts/jobs.json`.

*(Bonus)*  
Capture the API response details for job search results and save to `artifacts/network.log`.

---

### **Task C — Code Quality & Diagnostics**
- Use event-based waits (`expect(locator).toBeVisible()`, networkIdle) — avoid hard sleeps.  
- Configure **trace, video, and screenshot** capture on failure.  
- Store outputs under `artifacts/`.

---

### Your `README.md` should include:
- How to install and run:
  ```bash
  npm install
  npx playwright install
  npx playwright test
  ```
- How to view reports:
  ```bash
  npx playwright show-report
  ```
- Notes on selector strategy, fallback usage, and CI setup.

---

## 🧱 Example `playwright.config.ts`

```ts
import { defineConfig, devices } from '@playwright/test';

export default defineConfig({
  testDir: './tests',
  timeout: 45000,
  expect: { timeout: 10000 },
  retries: 1,
  reporter: [['html', { outputFolder: 'playwright-report' }], ['list']],
  use: {
    baseURL: 'https://www.upwork.com',
    headless: true,
    trace: 'on-first-retry',
    video: 'retain-on-failure',
    screenshot: 'only-on-failure',
  },
  projects: [
    { name: 'chromium', use: { ...devices['Desktop Chrome'] } },
  ],
});
```

---

## ✅ Evaluation Criteria (100 pts)

| Category | Points |
|-----------|---------|
| Test strategy & documentation | 20 |
| Robust selectors & waits | 25 |
| Functional coverage (Tasks A & B) | 25 |
| Code architecture & readability | 20 |
| Diagnostics & reporting | 10 |


**Passing score:** 75 or higher.

---

## 🧭 Tips
- Keep your code clean and DRY.  
- Avoid arbitrary waits (`waitForTimeout`).  
- Focus on *stability and clarity*, not just coverage.  
- Include screenshots, traces, and reports to showcase your debugging approach.  
- Be gentle with the target site — no spamming or unnecessary requests.

---

## 📤 Submission
When you’re done:
1. Push your code to a **private GitHub repo**.  
2. Include a short note about:
   - Your test strategy  
   - Selector approach  
   - Any issues or fallbacks used  
3. Invite deby@gigradar.io to your GitHub repo.

Thank you for taking the time to complete this assessment 🙏  
We’re looking forward to seeing how you structure your tests and handle real-world web automation challenges.
