---
title: git switch
description: "git switch i Kommandon — Git-boken av Marcus Ackre Medina"
parent: Kommandon
nav_order: 50
---

# git switch

Byt branch. Det moderna alternativet till `git checkout` för just det syftet.

```bash
git switch main
git switch feature/rabattkod
```

## Skapa och byt i ett steg

```bash
git switch -c feature/login
```

`-c` = create. Skapar branchen och byter till den. Det vanligaste sättet att starta ny feature-branch.

## Gå tillbaka till föregående branch

```bash
git switch -
```

Bindestreck fungerar precis som `cd -` i terminalen — tar dig tillbaka dit du var. Bra för att studsa mellan två branches.

## Varför inte `git checkout`?

`git checkout` gör för många saker — det byter branch, återställer filer, och checkar ut specifika commits. Det förvirrar ofta nybörjare.

`git switch` gör bara en sak: byta branch. `git restore` gör den andra saken (återställa filer). Tydligare uppdelning.

Båda fungerar. `git switch` är den moderna syntaxen sedan Git 2.23 (2019).

## Hämta en remote branch lokalt

```bash
git switch -c feature/login origin/feature/login
```

Skapar en lokal branch som trackar remote-branchen. Eller kortare:

```bash
git switch --track origin/feature/login
```
