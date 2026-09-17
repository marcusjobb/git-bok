---
title: git fetch
parent: Kommandon
nav_order: 90
---

# git fetch

```mermaid
flowchart LR
    WD["Working Directory"]
    ST["Stash"]
    SA["Staging Area"]
    LR["**Local Repository**"]
    RE[("**Remote**\n(GitHub)")]

    WD <-->|stash / pop| ST
    WD -->|git add| SA
    SA -->|git commit| LR
    LR -->|git push| RE
    RE -->|git fetch| LR
    LR -.->|git merge| WD

    style LR fill:#1565c0,stroke:#0d47a1,color:#fff
    style RE fill:#1565c0,stroke:#0d47a1,color:#fff
```

Hämta ändringar från remote — utan att röra din lokala kod.

```bash
git fetch
git fetch origin          # hämta från origin specifikt
git fetch --all           # hämta från alla remotes
```

## Vad är skillnaden mot `git pull`?

`git pull` = `git fetch` + `git merge`. Det hämtar **och** integrerar ändringarna direkt.

`git fetch` hämtar bara — du bestämmer själv vad som händer sen. Bra om du vill se vad som hänt på remote innan du bestämmer dig för att mergea.

```bash
git fetch
git log HEAD..origin/main    # se commits på remote som du inte har lokalt
git diff HEAD origin/main    # se exakt vad som skiljer sig
git merge origin/main        # mergea när du är redo
```

## Håll koll på vad som hänt

```bash
git fetch
git log --oneline origin/main -10    # de senaste 10 commits på main
```

Bra i början av dagen — kolla vad kollegorna pushat under natten innan du börjar jobba.

## Fetch och remote-tracking branches

När du kör `git fetch` uppdateras `origin/main`, `origin/feature/rabattkod` och liknande — de lokala kopiorna av remote-brancherna. De ändras **aldrig** automatiskt, bara via fetch. Din lokala `main` är opåverkad tills du faktiskt mergear.
