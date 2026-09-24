---
title: git reset
description: "Ångra saker. Det här kommandot har tre lägen med väldigt olika konsekvenser — läs innan du kör."
parent: Kommandon
nav_order: 130
---

# git reset

Ångra saker. Det här kommandot har tre lägen med väldigt olika konsekvenser — läs innan du kör.

## Ångra staging (ofarligt)

```bash
git reset HEAD Kassan.cs        # äldre syntax
git restore --staged Kassan.cs  # modern syntax, föredra den här
```

Tar bort filen från staging area. Ingenting i working directory påverkas — koden är kvar, den ingår bara inte i nästa commit längre.

## Ångra commits — `--soft` (ofarligt)

```bash
git reset --soft HEAD~1
```

Ångrar den senaste committen men **behåller ändringarna stagade**. Bra om du råkade committa för tidigt och vill lägga till mer.

`HEAD~1` = en commit bakåt. `HEAD~3` = tre commits bakåt.

```mermaid
flowchart LR
    A[Commit C] -->|git reset --soft HEAD~1| B[Staging Area]
    B --> C[Commit C igen, med mer]
    style B fill:#f0f0f0,stroke:#888,color:#111
```

## Ångra commits — `--mixed` (standard, försiktig)

```bash
git reset HEAD~1
git reset --mixed HEAD~1   # samma sak
```

Ångrar committen och unstagar ändringarna — men behåller koden i working directory. Du får bestämma vad som ska committas igen.

## Ångra commits — `--hard` (destruktivt)

```bash
git reset --hard HEAD~1
```

Ångrar committen **och kastar bort alla ändringar**. Koden är borta. Working directory återgår till tillståndet i föregående commit.

Kör inte `--hard` utan att vara säker på att du inte behöver koden. Och kör aldrig `--hard` på commits du redan pushat — då skriver du om historiken som andra bygger på.

Om du råkade köra `--hard` och vill ha tillbaka koden: titta på [`git reflog`](reflog.md) — det finns ofta en väg tillbaka.

## Sammanfattning

| Flagga | Committen | Staging area | Working directory |
|--------|-----------|--------------|-------------------|
| `--soft` | Ångras | Behålls (stagat) | Behålls |
| `--mixed` | Ångras | Rensas | Behålls |
| `--hard` | Ångras | Rensas | **Rensas** |
