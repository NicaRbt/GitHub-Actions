# 🚀 GitHub Actions – Workflow Events

## 📌 Overview

GitHub Actions permite declanșarea (triggering) workflow-urilor în mai multe moduri, în funcție de evenimentele din repository sau acțiuni externe.

---

# 🔹 1. Repository Events

Aceste evenimente sunt declanșate automat de acțiuni din repository.

## 🟢 push

Declanșat atunci când cineva face push în repository.

### Exemplu:

```yaml
on:
  push:
```

### Use case:

* Build automat după fiecare commit
* Rulare teste

---

## 🟢 issues

Declanșat de evenimente legate de issue-uri.

### Exemple de evenimente:

* opened
* closed
* edited

### Exemplu:

```yaml
on:
  issues:
    types: [opened, closed]
```

### Use case:

* Automatizare task-uri issue
* Notificări

---

## 🟢 pull_request

Declanșat la evenimente legate de Pull Requests.

### Exemple:

* opened
* synchronize
* closed

### Exemplu:

```yaml
on:
  pull_request:
    types: [opened, synchronize]
```

### Use case:

* Validare cod înainte de merge
* CI/CD pipeline

---

## 🟢 pull_request_review

Declanșat la review-uri pe PR.

### Exemple:

* submitted
* edited
* dismissed

### Exemplu:

```yaml
on:
  pull_request_review:
    types: [submitted]
```

### Use case:

* Acțiuni după aprobarea codului
* Workflow pentru code review

---

## 🟢 fork

Declanșat când repository-ul este fork-uit.

### Exemplu:

```yaml
on:
  fork:
```

### Use case:

* Monitorizare fork-uri
* Analytics

---

# 🔹 2. Manual Triggers

Acestea permit rularea manuală sau externă a workflow-urilor.

---

## 🟡 workflow_dispatch (UI Trigger)

Permite rularea manuală din GitHub UI (Actions tab).

### Exemplu:

```yaml
on:
  workflow_dispatch:
```

### Use case:

* Rulare manuală deployment
* Debugging

---

## 🟡 repository_dispatch (API Trigger)

Declanșat prin API GitHub.

### Exemplu:

```yaml
on:
  repository_dispatch:
    types: [custom-event]
```

### Use case:

* Integrare cu alte sisteme
* Automatizare externă

---

## 🟡 workflow_call (Triggered from another workflow)

Permite apelarea unui workflow din alt workflow.

### Exemplu:

```yaml
on:
  workflow_call:
```

### Use case:

* Reutilizare workflow-uri
* Modularizare CI/CD

---

# 🔹 3. Schedule (Cron Jobs)

Rulează workflow-ul la intervale definite.

## 🟠 schedule

Execută job-uri pe bază de cron.

### Exemplu:

```yaml
on:
  schedule:
    - cron: "0 0 * * *"
```

### Explicație cron:

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

### Use case:

* Backup zilnic
* Job-uri recurente
* Monitorizare

---

# 📊 Rezumat

| Tip Trigger      | Exemplu             | Utilizare         |
| ---------------- | ------------------- | ----------------- |
| Repository Event | push, PR            | CI/CD automat     |
| Manual           | workflow_dispatch   | Rulare manuală    |
| API              | repository_dispatch | Integrare externă |
| Workflow         | workflow_call       | Reutilizare       |
| Schedule         | cron                | Job-uri periodice |

---

# ✅ Best Practices

* 🔹 Folosește `push` + `pull_request` pentru CI complet
* 🔹 Adaugă `workflow_dispatch` pentru debugging
* 🔹 Utilizează `workflow_call` pentru DRY (Don't Repeat Yourself)
* 🔹 Evită rulările inutile (filtre pe branch-uri)

---

# 🎯 Exemplu complet

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

# 📚 Concluzie

GitHub Actions oferă flexibilitate mare prin multiple tipuri de trigger:

* automate (push, PR)
* manuale
* programate
* externe

Alegerea corectă depinde de nevoile pipeline-ului tău.
