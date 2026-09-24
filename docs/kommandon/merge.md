---
title: git merge
description: "Slå ihop två branches. Du är på branchen som ska ta emot ändringarna och anger branchen som ska mergas in."
parent: Kommandon
nav_order: 120
---

# git merge

Slå ihop två branches.

```bash
git switch main
git merge feature/rabattkod
```

Du är på branchen som ska **ta emot** ändringarna och anger branchen som ska **mergas in**.

## Fast-forward merge

Om `main` inte har några nya commits sedan feature-branchen skapades behövs ingen merge-commit — Git "spolar bara framåt":

```mermaid
%%{init: { 'gitGraph': {'mainBranchName': 'main'}} }%%
gitGraph
    commit id: "A"
    branch feature/rabattkod
    commit id: "B"
    commit id: "C"
    checkout main
    merge feature/rabattkod
```

Resultatet ser ut som om du alltid jobbat direkt på `main`. Ingen extra commit.

## Three-way merge

Om `main` har fått egna commits medan du jobbat på feature-branchen skapar Git en merge-commit:

```mermaid
%%{init: { 'gitGraph': {'mainBranchName': 'main'}} }%%
gitGraph
    commit id: "A"
    branch feature/rabattkod
    commit id: "B"
    checkout main
    commit id: "C"
    merge feature/rabattkod id: "Merge"
```

## Tvinga merge-commit

```bash
git merge --no-ff feature/rabattkod
```

Skapar alltid en merge-commit, även om fast-forward vore möjlig. Bra om du vill att historiken tydligt ska visa att en feature-branch mergades.

## Avbryta en merge

Är du mitt i en merge med konflikter och vill backa?

```bash
git merge --abort
```

Återställer allt till läget innan merge påbörjades.

Se [Merge-konflikter](../konflikter/merge-konflikt.md) om du fastnar i konflikter.
