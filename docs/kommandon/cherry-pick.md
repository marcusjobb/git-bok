---
title: git cherry-pick
description: "Plocka in en specifik commit från en annan branch — utan att mergea hela branchen."
parent: Kommandon
nav_order: 145
---

# git cherry-pick

Plocka in en specifik commit från en annan branch — utan att mergea hela branchen.

```bash
git cherry-pick a3f8c21
```

Det skapar en ny commit på din nuvarande branch med exakt samma ändringar som `a3f8c21`, men med en ny hash.

## När det är användbart

**Scenario:** Du jobbade på `feature/rabattkod` och fixade en bugg längs vägen. Buggen är akut — den behöver till `main` nu, men feature-branchen är inte klar.

```bash
git switch main
git cherry-pick <hash på buggfixen>
git push
```

Nu är buggen fixad i `main` utan att du behöver mergea den halvfärdiga feature-branchen.

**Scenario 2:** Du committade på fel branch av misstag.

```bash
git log --oneline -1    # notera hash på din commit
git switch rätt-branch
git cherry-pick <hash>
git switch fel-branch
git reset --hard HEAD~1  # ta bort committen från fel branch
```

## Flera commits i rad

```bash
git cherry-pick a3f8c21 9d2e1f0    # två specifika commits
git cherry-pick a3f8c21..9d2e1f0   # ett intervall (exkluderar första)
git cherry-pick a3f8c21^..9d2e1f0  # ett intervall (inkluderar första)
```

## Om det uppstår konflikter

Cherry-pick kan skapa konflikter — precis som merge. Lös dem, staga filerna och fortsätt:

```bash
git cherry-pick --continue
```

Eller avbryt:

```bash
git cherry-pick --abort
```

## Snabbvarning

Cherry-pick skapar **dubbletter av commits** — samma förändring finns nu på två ställen med olika hash. Det kan förvirra `git log` och skapa konflikter längre fram om du sedan också mergear branchen. Använd det med urskillning — det är ett kirurgiskt verktyg, inte en rutin.
