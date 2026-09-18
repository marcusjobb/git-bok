---
title: GitHub Flow
description: "GitHub Flow i Branching-strategier — Git-boken av Marcus Ackre Medina"
parent: Branching-strategier
nav_order: 20
---

# GitHub Flow

## Grundidén

GitHub Flow är Git Flows enkla motsats — **en** permanent branch (`main`) och korta, kortlivade feature branches. Ingen `develop`, ingen `release/*`, ingen `hotfix/*`. Allt som mergas till `main` ska kunna deployas direkt.

```mermaid
%%{init: { 'gitGraph': {'mainBranchName': 'main'}} }%%
gitGraph
    commit id: "v1"
    branch feature/sok-funktion
    checkout feature/sok-funktion
    commit id: "Lägg till sökfält"
    commit id: "Koppla mot API"
    checkout main
    merge feature/sok-funktion tag: "deploy"
    branch feature/dark-mode
    checkout feature/dark-mode
    commit id: "Dark mode toggle"
    checkout main
    merge feature/dark-mode tag: "deploy"
```

## Flödet i fem steg

1. **Branch:a ut från `main`** — namnge branchen beskrivande: `feature/sok-funktion`, `fix/krasch-vid-inloggning`
2. **Committa och pusha ofta** — så teamet kan följa med och ge feedback tidigt
3. **Öppna en Pull Request** — även innan koden är helt klar, för tidig diskussion
4. **Granska och diskutera** — teamet kommenterar, CI-tester körs automatiskt
5. **Mergea till `main` och deploya** — så fort PR:en är godkänd

```mermaid
flowchart LR
    A[Branch:a från main] --> B[Committa & pusha]
    B --> C[Öppna Pull Request]
    C --> D[Kodgranskning + CI]
    D -->|Godkänd| E[Merge till main]
    E --> F[Deploy]
    D -->|Ändringar behövs| B
    style E fill:#1565c0,stroke:#0d47a1,color:#fff
    style F fill:#e8f5e9,stroke:#2e7d32,color:#111
```

## Varför fungerar det utan develop/release-grenar?

Förutsättningen är att `main` **alltid** är deploybar — det säkerställs av automatiserade tester i CI/CD-pipelinen, inte av en separat integrationsgren. Istället för att samla upp features i `develop` och testa allt tillsammans innan en stor release, testas varje liten förändring för sig, direkt innan den mergas.

## Fördelar och nackdelar

**Fördelar:**
- Enkelt att förstå — en regel: `main` är alltid deploybar
- Passar perfekt för **kontinuerlig leverans** (flera deploys om dagen)
- Färre branches att hålla reda på, mindre administration

**Nackdelar:**
- Kräver bra CI/CD och testtäckning — utan det blir "main alltid deploybar" ett tomt löfte
- Inga separata release-versioner att peka på om du behöver supportera flera versioner parallellt hos olika kunder
- Ingen inbyggd plats för större, riskfyllda förändringar som behöver mogna över tid innan de släpps

## När passar GitHub Flow?

Webbtjänster och SaaS-produkter som deployar kontinuerligt till en enda produktionsmiljö — precis den typen av projekt GitHub själva byggde modellen för. Passar sämre för produkter med schemalagda versionssläpp eller flera parallellt supporterade versioner, där [Git Flow](git-flow.md) ger tydligare struktur.
