---
title: Committade på fel branch
parent: Scenarios
nav_order: 10
---

# Committade på fel branch

Det händer alla. Du jobbar intensivt, glömmer att byta branch, och committar direkt på `main`. Eller på fel feature-branch. Ingen fara — det är fixbart.

## Scenario 1: En commit på fel branch, inte pushad

Du är på `main` och har gjort en commit som borde vara på `feature/rabattkod`.

```bash
git log --oneline -3
# a3f8c21 feat: lägg till rabattkod-validering   ← den här ska bort härifrån
# 9d2e1f0 fix: förhindra krasch vid tom kundvagn
# 7b4a3c8 feat: lägg till kundvagn
```

**Steg 1:** Notera hash på committen (`a3f8c21`).

**Steg 2:** Skapa (eller byt till) rätt branch — branchen pekar nu på `a3f8c21`, precis som `main`.

```bash
git switch -c feature/rabattkod
```

**Steg 3:** Gå tillbaka till `main` och ta bort committen där.

```bash
git switch main
git reset --hard HEAD~1
```

`HEAD~1` = en commit bakåt. `main` pekar nu på `9d2e1f0` — som om committen aldrig hänt på `main`.

Klar. Committen finns kvar på `feature/rabattkod`.

---

## Scenario 2: Flera commits på fel branch, inte pushade

Du har gjort tre commits på `main` som borde vara på en feature-branch.

```bash
git log --oneline -5
# c1d2e3f feat: rabattkod i kundvagn     ← dessa tre
# b0a9f8e feat: rabattkod-validering     ← ska till
# a3f8c21 feat: rabattkod-input          ← feature-branch
# 9d2e1f0 fix: förhindra krasch          ← härifrån var main OK
```

**Steg 1:** Skapa feature-branchen från nuvarande HEAD (alla tre commits följer med).

```bash
git switch -c feature/rabattkod
```

**Steg 2:** Gå tillbaka till `main`, backa tre commits.

```bash
git switch main
git reset --hard HEAD~3
```

---

## Scenario 3: Committade på fel branch, redan pushad

Det svårare läget. Du har pushat till `main` och det du pushade ska egentligen till en feature-branch.

**Steg 1:** Skapa feature-branchen från din nuvarande position (tar med commits).

```bash
git switch -c feature/rabattkod
git push -u origin feature/rabattkod
```

**Steg 2:** På `main` — revert istället för reset, eftersom andra kan ha hämtat.

```bash
git switch main
git revert a3f8c21   # skapa en revert-commit för varje commit som ska bort
git push
```

Nu är `main` tillbaka till rätt läge, utan att du skrivit om historiken som andra bygger på.

---

## Snabbguide

| Situation | Lösning |
|-----------|---------|
| Inte pushad, en commit | `git switch -c ny-branch` → `git switch main` → `git reset --hard HEAD~1` |
| Inte pushad, flera commits | Samma, men `HEAD~N` |
| Redan pushad | `git switch -c ny-branch` + `git push` → `git revert` på main |
