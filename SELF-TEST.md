# Self-Test: Conceptual Assessment

> Part of the **Self-Learning Advanced** assessment evidence (INFO1111, Semester 1 2026)

As this course did not include built-in section quizzes, I designed and completed my own 10-question conceptual self-assessment after finishing the hands-on project, answering entirely from memory with no reference material.

**Result: 10/10 answered correctly.** Questions 6 and 7 were answerable with confidence specifically because I had personally diagnosed and resolved both underlying pipeline failures during the hands-on project (see the [Self-Learning Advanced report](#) for the full debugging history and screenshots).

---

### Q1: What does CI stand for, and what does CD stand for (both meanings)?

CI = Continuous Integration. CD = Continuous Delivery (automated build/test/package, manual release trigger) or Continuous Deployment (fully automated release with no manual approval).

---

### Q2: What's the difference between a job and a step in a GitHub Actions workflow?

A job is a set of steps running on the same runner; jobs run in parallel by default unless dependencies are set. A step is a single task within a job; steps in the same job run sequentially and share filesystem/state.

---

### Q3: What keyword makes one job wait for another to finish first?

`needs:`, e.g. a deploy job specifying `needs: test` will only run after the test job completes successfully.

---

### Q4: What's the difference between a GitHub Secret and a regular environment variable?

A regular env var is plain text, visible in logs and stored directly in the workflow file. A Secret is encrypted at rest, stored in GitHub settings rather than the repo, automatically masked in logs, and injected at runtime via `secrets.NAME` — used for API keys, tokens and passwords.

---

### Q5: What triggers a workflow on every pull request, and which YAML key controls this?

The `on:` key, specifically `on: pull_request:`, which fires on PR events such as open, sync and reopen.

---

### Q6: Why did the lint job fail the first time ESLint was added?

The installed ESLint version (v9+) uses the newer "flat config" format and no longer reads the legacy `.eslintrc.json` file by default, so it had no valid configuration to run against and exited with a fatal error (exit code 2) rather than checking any code.

---

### Q7: Why did the deploy job fail the second time, even after lint and test passed?

The third-party GitHub Action used to deploy (`amondnet/vercel-action`) had an old, pinned Vercel CLI version (25.1.0) bundled inside it. Vercel's servers had since raised the minimum required CLI version to 47.2.2 and rejected the outdated CLI. The fix was to stop using that action and install the latest Vercel CLI directly in the workflow instead.

---

### Q8: What's the difference between a JavaScript-based and a Docker-based custom action?

A JavaScript action runs directly on the runner using Node.js, with fast startup but limited to what the runner OS/Node supports. A Docker action runs inside its own container, offering more flexibility (any language or dependency) but slower startup and Linux-runner-only support.

---

### Q9: What is a service container used for in GitHub Actions?

A Docker container spun up alongside a job's main container to provide a dependency the job needs, such as a database or cache, used when tests need to talk to a real service rather than a mock.

---

### Q10: How would you cache `node_modules` between workflow runs?

Using the `actions/cache` action, or the built-in `cache: 'npm'` option in `actions/setup-node`, typically keyed on the hash of `package-lock.json` so installs are skipped when dependencies haven't changed.

---

*INFO1111 Semester 1, 2026 — The University of Sydney*
