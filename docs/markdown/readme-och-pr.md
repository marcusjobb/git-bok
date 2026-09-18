---
title: README och Pull Request
description: "README och Pull Request i Markdown & README — Git-boken av Marcus Ackre Medina"
parent: Markdown & README
nav_order: 20
---

# README och Pull Request

## README.md

README är projektets välkomstsida — den fil GitHub visar automatiskt när någon besöker ett repo. Varje projekt ska ha en.

En bra README innehåller:

1. **Vad projektet är** — en mening
2. **Hur man kör det** — steg för steg
3. **Vad man behöver** — förutsättningar (t.ex. .NET 10)
4. **Vem som gjort det** — och eventuell licens

````markdown
# Gissningsspel

Ett enkelt terminalspel i C# där du gissar ett hemligt tal.

## Krav

- .NET 10 SDK

## Kör spelet

```bash
git clone git@github.com:dittnamn/gissningsspel.git
cd gissningsspel
dotnet run
```

## Regler

Gissa ett tal mellan 1 och 100. Du får veta om din gissning är för högt eller för lågt.
````

README skrivs alltid i Markdown och heter alltid `README.md` — med versaler, för det är konvention.

## Pull Request

En Pull Request (PR) är en förfrågan att mergea en branch till en annan — och en möjlighet för teamet att granska koden innan den hamnar i huvudgrenen. Det är GitHubs funktion, inte Gits.

```mermaid
flowchart TD
    A["Du: push feature/login"] --> B["Öppna Pull Request på GitHub"]
    B --> C["Kollega granskar koden\nlämnar kommentarer"]
    C --> D{Godkänd?}
    D -->|Ja| E["Merge till main"]
    D -->|Nej, ändringar behövs| F["Du fixar, pushar igen"]
    F --> C
    style E fill:#1565c0,stroke:#0d47a1,color:#fff
```

En PR innehåller vanligtvis: en titel, en beskrivning av vad som ändrades och varför, och eventuellt skärmdumpar om det är UI-ändringar. Allt detta skrivs i — Markdown.

**Vad gör en bra PR-beskrivning?** Samma regel som commit-meddelanden: förklara **varför**, inte bara vad. En granskare som förstår syftet kan ge bättre feedback än en som bara ser en diff.

## Sammanfattning: Git-arbetsflödet

```mermaid
flowchart TD
    A["git pull\nhämta det senaste"] --> B["Skriv kod\nändra filer"]
    B --> C["git status\nse vad som ändrats"]
    C --> D["git add filnamn.cs\nförbered för commit"]
    D --> E["git commit -m 'beskrivning'\nspara ögonblicksbild"]
    E --> F["git push\nskicka till GitHub"]
    F --> G["Pull Request\ngranskning och merge"]
    style E fill:#1565c0,stroke:#0d47a1,color:#fff
    style F fill:#1565c0,stroke:#0d47a1,color:#fff
    style G fill:#e8f5e9,stroke:#2e7d32,color:#111
```
