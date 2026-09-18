---
title: git reflog
description: "git reflog i Kommandon — Git-boken av Marcus Ackre Medina"
parent: Kommandon
nav_order: 150
---

# git reflog

Den sista räddningsplankan. (Och nej, det har inget med 50 shades att göra.)

`git log` visar historiken för projektet. `git reflog` visar historiken för **vad du gjort** — varje gång HEAD rört sig, oavsett om det syns i `git log` eller inte.

```bash
git reflog
```

```plaintext
a3f8c21 HEAD@{0}: commit: feat: lägg till rabattkod-validering
9d2e1f0 HEAD@{1}: reset: moving to HEAD~1
7b4a3c8 HEAD@{2}: commit: fix: förhindra krasch vid tom kundvagn
b5c2d1e HEAD@{3}: checkout: moving from main to feature/rabattkod
```

Allt finns här: commits, resets, checkouts, rebases, merges.

## Varför är det en räddningsplanka?

Körde du `git reset --hard` på fel commit? Tappade en branch? Förstörde något med en rebase?

Reflog minns. Och du kan återställa.

```bash
git reflog                     # hitta commit-hashen du vill tillbaka till
git reset --hard HEAD@{2}      # gå tillbaka till det läget
```

eller

```bash
git checkout -b räddad-branch 7b4a3c8   # skapa en ny branch från den gamla committen
```

## Hur länge sparas reflog?

Som standard 90 dagar. Det räcker för de flesta "åh nej vad hände"-situationer. Reflog är lokal — den pushas inte till GitHub.

## Vanliga räddningsscenarier

| Vad hände | Lösning |
|-----------|---------|
| `git reset --hard` på fel commit | `git reflog` → hitta committen → `git reset --hard HEAD@{N}` |
| Tappade en branch jag inte mergate | `git reflog` → hitta sista committen → `git checkout -b ny-branch <hash>` |
| Rebasen gick helt fel | `git reflog` → hitta ORIG_HEAD → `git reset --hard ORIG_HEAD` |

Git slänger nästan ingenting. Reflog är beviset.
