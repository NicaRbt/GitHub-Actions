# 🚀 GitHub Actions – Workflow Events

## 📌 Overview

GitHub Actions allows you to trigger workflows in multiple ways, depending on repository events or external actions.

---

# 🔹 1. Repository Events

These events are automatically triggered by actions happening in your repository.

## 🟢 push

Triggered when someone pushes code to the repository.

### Example:

```yaml
on:
  push:
```

### Use cases:

* Automatically build after each commit
* Run tests

---

## 🟢 issues

Triggered by events related to issues.

### Event types:

* opened
* closed
* edited

### Example:

```yaml
on:
  issues:
    types: [opened, closed]
```

### Use cases:

* Automate issue handling
* Send notifications

---

## 🟢 pull_request

Triggered by events related to pull requests.

### Event types:

* opened
* synchronize
* closed

### Example:

```yaml
on:
  pull_request:
    types: [opened, synchronize]
```

### Use cases:

* Validate code before merging
* Run CI/CD pipelines

---

## 🟢 pull_request_review

Triggered by pull request review events.

### Event types:

* submitted
* edited
* dismissed

### Example:

```yaml
on:
  pull_request_review:
    types: [submitted]
```

### Use cases:

* Trigger actions after approval
* Enforce review workflows

---

## 🟢 fork

Triggered when your repository is forked.

### Example:

```yaml
on:
  fork:
```

### Use cases:

* Monitor repository forks
* Collect analytics

---

# 🔹 2. Manual Triggers

These allow workflows to be triggered manually or from external systems.

---

## 🟡 workflow_dispatch (UI Trigger)

Allows manual execution from the GitHub UI (Actions tab).

### Example:

```yaml
on:
  workflow_dispatch:
```

### Use cases:

* Manual deployments
* Debugging workflows

---

## 🟡 repository_dispatch (API Trigger)

Triggered via GitHub API.

### Example:

```yaml
on:
  repository_dispatch:
    types: [custom-event]
```

### Use cases:

* Integration with external systems
* Trigger workflows from other services

---

## 🟡 workflow_call (Triggered from another workflow)

Allows one workflow to call another.

### Example:

```yaml
on:
  workflow_call:
```

### Use cases:

* Reusable workflows
* Modular CI/CD pipelines

---

# 🔹 3. Schedule (Cron Jobs)

Runs workflows at defined time intervals.

## 🟠 schedule

Executes jobs based on a cron schedule.

### Example:

```yaml
on:
  schedule:
    - cron: "0 0 * * *"
```

### Cron format:

```
┌───────────── minute (0 - 59)
│ ┌───────────── hour (0 - 23)
│ │ ┌───────────── day of month (1 - 31)
│ │ │ ┌───────────── month (1 - 12)
│ │ │ │ ┌───────────── day of week (0 - 6)
│ │ │ │ │
│ │ │ │ │
* * * * *
```

### Use cases:

* Daily backups
* Scheduled jobs
* Monitoring tasks

---

# 📊 Summary

| Trigger Type     | Example             | Usage                 |
| ---------------- | ------------------- | --------------------- |
| Repository Event | push, PR            | Automated CI/CD       |
| Manual           | workflow_dispatch   | Manual execution      |
| API              | repository_dispatch | External integrations |
| Workflow         | workflow_call       | Reusability           |
| Schedule         | cron                | Periodic jobs         |

---

# ✅ Best Practices

* 🔹 Use `push` + `pull_request` for full CI coverage
* 🔹 Add `workflow_dispatch` for debugging
* 🔹 Use `workflow_call` to avoid duplication (DRY principle)
* 🔹 Limit unnecessary runs (use branch filters)

---

# 🎯 Complete Example

```yaml
name: CI Pipeline

on:
  push:
    branches: [main]
  pull_request:
  workflow_dispatch:
  schedule:
    - cron: "0 0 * * 1"

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Running pipeline"
```

---

# 📚 Conclusion

GitHub Actions provides great flexibility through multiple trigger types:

* Automated (push, pull_request)
* Manual
* Scheduled
* External

Choosing the right trigger depends on your pipeline requirements.
