# Self-Learning Advanced: CI/CD Pipeline

> **Unit:** INFO1111 — Computing 1A Professionalism
> **Semester:** Semester 1, 2026
> **University:** The University of Sydney
> **Student:** Lakshya Sakhuja (540863213)

---

## 📋 Project Overview

This repository is the hands-on evidence for my **Self-Learning Advanced** assessment, building on the topic chosen in my Self-Learning Foundation report: **learning CI/CD pipelines with automated deployment and testing using GitHub Actions and Vercel**.

It contains a small JavaScript application with a complete, working CI/CD pipeline that automatically lints, tests, and deploys the code to production every time changes are pushed to `main`.

This was built after completing the 11-section Udemy course *"GitHub Actions – The Complete Guide"* by Maximilian Schwarzmüller, and applies that learning to a real working system rather than a tutorial copy.

---

## 🔧 Pipeline Architecture

The pipeline runs as three sequential jobs, each depending on the previous one passing:

| Job | Purpose | Depends On |
|---|---|---|
| `lint` | Runs ESLint against the codebase to enforce code quality | — |
| `test` | Runs the Jest test suite (unit tests for core logic) | `lint` |
| `deploy` | Installs the Vercel CLI and deploys to production (main branch only) | `test` |

If any job fails, later jobs do not run — this was deliberately tested and confirmed during development (see the Self-Learning Advanced report for the full debugging history).

---

## 🛠 Tech Stack

| Tool | Purpose |
|---|---|
| **GitHub Actions** | CI/CD automation engine |
| **Jest** | JavaScript unit testing framework |
| **ESLint** | Code quality / linting |
| **Vercel** | Deployment platform |
| **Node.js** | Runtime |

---

## 📁 Repository Structure

```
cicd-learning-demo/
├── .github/
│   └── workflows/
│       └── ci.yml          # The full lint → test → deploy pipeline
├── math.js                 # Application logic
├── math.test.js            # Jest unit tests
├── index.html               # Static page deployed to Vercel
├── eslint.config.js        # ESLint flat config
├── package.json
└── README.md
```

---

## 🚀 Live Deployment

The pipeline automatically deploys to:

**[https://info1111-pi.vercel.app](https://info1111-pi.vercel.app)**

Every successful push to `main` redeploys this URL automatically — no manual deployment steps are involved.

---

## 💻 Running Locally

```bash
git clone https://github.com/lakshyasakhuja/cicd-learning-demo.git
cd cicd-learning-demo
npm install
npm test        # run the Jest test suite
npm run lint     # run ESLint
```

---

## 📚 Learning Resources Used

- [GitHub Actions Official Documentation](https://docs.github.com/en/actions)
- [Vercel Documentation — Git Integration](https://vercel.com/docs/deployments/git)
- [GitHub Actions – The Complete Guide (Udemy)](https://www.udemy.com/course/github-actions-the-complete-guide/) — **completed in full**, certificate included in the Self-Learning Advanced report appendix
- [freeCodeCamp CI/CD with GitHub Actions Tutorial](https://www.youtube.com/watch?v=R8_veQiYBjI)

---

## ✅ Assignment Evidence Checklist

- [x] Working CI/CD pipeline with automated testing
- [x] Code linting integrated into the pipeline
- [x] Genuine production deployment via Vercel
- [x] Secrets managed securely using GitHub Secrets (not committed to the repo)
- [x] Real debugging history documented (2 genuine failures, both resolved)
- [x] Self-test conceptual assessment completed (10/10)
- [x] Course completed in full with certificate of completion

---

## 🔗 Useful Links

- [Self-Learning Foundation Report](#) — original topic, resources, and assessment plan
- [Self-Learning Advanced Report](#) — full reflection and evidence
- [Canvas Submission Page](https://canvas.sydney.edu.au)
- [Ed Discussion Board](https://edstem.org)

---

*INFO1111 Semester 1, 2026 — The University of Sydney*
