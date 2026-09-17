---
title: git branch
parent: Kommandon
nav_order: 40
---

# git branch

Hantera branches — lista, skapa och ta bort.

## Lista branches

```bash
git branch           # lokala branches
git branch -r        # remote branches
git branch -a        # alla (lokala + remote)
```

```plaintext
* feature/rabattkod
  main
  fix/krasch-vid-tom-kundvagn
```

`*` markerar den branch du är på just nu.

## Skapa en branch

```bash
git branch feature/login          # skapa (men byt inte till den)
git switch -c feature/login       # skapa och byt till den — det vanliga
git checkout -b feature/login     # äldre syntax, samma sak
```

## Byta branch

```bash
git switch main
git checkout main    # äldre syntax
```

Se [`git switch`](switch.md) för mer.

## Ta bort en branch

```bash
git branch -d feature/rabattkod       # ta bort (om den är mergad)
git branch -D feature/rabattkod       # tvinga bort (även om den inte är mergad)
```

`-d` vägrar ta bort en branch med ändringar som inte mergats — skyddar mot att du råkar kasta bort kod av misstag. `-D` är `--force`, kör bara om du är säker.

Ta bort remote branch:

```bash
git push origin --delete feature/rabattkod
```

## Byta namn på en branch

```bash
git branch -m gammalt-namn nytt-namn    # byt namn lokalt
git push origin --delete gammalt-namn   # ta bort det gamla namnet på remote
git push -u origin nytt-namn            # push med nytt namn
```
