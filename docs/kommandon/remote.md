---
title: git remote
description: "git remote i Kommandon — Git-boken av Marcus Ackre Medina"
parent: Kommandon
nav_order: 85
---

# git remote

```mermaid
flowchart LR
    WD["Working Directory"]
    ST["Stash"]
    SA["Staging Area"]
    LR["Local Repository"]
    RE[("**Remote**\n(GitHub)")]

    WD <-->|stash / pop| ST
    WD -->|git add| SA
    SA -->|git commit| LR
    LR -->|git push| RE
    RE -->|git fetch| LR
    LR -.->|git merge| WD

    style RE fill:#1565c0,stroke:#0d47a1,color:#fff
```

Hantera kopplingar till fjärrrepon.

## Lista remotes

```bash
git remote -v
```

```plaintext
origin  git@github.com:marcusjobb/git-bok.git (fetch)
origin  git@github.com:marcusjobb/git-bok.git (push)
```

`-v` (verbose) visar URL:erna. Utan `-v` ser du bara namnen.

## Lägga till en remote

```bash
git remote add origin git@github.com:dittnamn/repo.git
```

`origin` är bara ett namn — konventionellt namnet för det primära fjärrrepot. Du kan kalla det vad som helst.

## Vanligt scenario — fork-arbetsflöde

Du forkat ett repo och vill kunna hämta uppdateringar från originalet:

```bash
git remote add upstream git@github.com:originalet/repo.git
git fetch upstream
git merge upstream/main
```

Nu har du två remotes: `origin` (din fork) och `upstream` (originalet).

## Byta URL på en remote

```bash
git remote set-url origin git@github.com:nyttnamn/repo.git
```

Behövs exempelvis om ett repo bytt namn eller om du byter från HTTPS till SSH.

## Ta bort en remote

```bash
git remote remove upstream
```

Påverkar inte det lokala repot — tar bara bort kopplingen.
