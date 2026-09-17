---
title: Vad är Actions?
parent: GitHub Actions
nav_order: 10
---

# Vad är GitHub Actions?

GitHub Actions är ett automatiseringssystem inbyggt direkt i GitHub. Du beskriver i en YAML-fil vad som ska hända och när — GitHub sköter resten på sina servrar.

Det vanligaste användningsområdet: **CI/CD** (Continuous Integration / Continuous Deployment). Kör testerna automatiskt varje gång någon pushar. Deploya till produktion automatiskt när en PR mergas till `main`.

## Grundbegreppen

```
Workflow
└── Job (körs på en runner)
    ├── Step 1: checkout kod
    ├── Step 2: installera .NET
    ├── Step 3: kompilera
    └── Step 4: kör tester
```

| Begrepp | Vad det är |
|---------|-----------|
| **Workflow** | En hel automatiseringsprocess, definierad i en YAML-fil |
| **Trigger** | Vad som startar workflow:en (`push`, `pull_request`, schema, manuellt) |
| **Job** | En grupp steg som körs tillsammans på samma maskin |
| **Step** | Ett enskilt kommando eller en action |
| **Runner** | Maskinen som kör jobbet (GitHub tillhandahåller Linux, Windows och macOS) |
| **Action** | Ett återanvändbart steg — antingen från GitHub Marketplace eller eget |

## Var bor workflow-filerna?

I repot, under `.github/workflows/`:

```
.github/
└── workflows/
    ├── ci.yml          ← kör tester vid varje push
    └── deploy.yml      ← deploya vid push till main
```

GitHub hittar dem automatiskt. Inga inställningar att klicka på.

## Triggers — när ska det köras?

```yaml
on:
  push:                        # vid varje push
    branches: [main]           # men bara till main
  pull_request:                # vid varje PR
    branches: [main]           # mot main
  schedule:
    - cron: '0 8 * * 1-5'     # måndag–fredag kl 08:00
  workflow_dispatch:           # manuell knapp i GitHub-gränssnittet
```

Du kan kombinera flera triggers i samma workflow.

## Gratis för open source

GitHub Actions är gratis för publika repos. För privata repos ingår 2 000 minuter per månad på gratisplanen — ett litet projekt kommer inte i närheten av det taket.
