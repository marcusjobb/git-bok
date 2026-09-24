---
title: Första workflow
description: "En minimal workflow som körs varje gång du pushar — och berättar om något gick fel."
parent: GitHub Actions
nav_order: 20
---

# Första workflow

En minimal workflow som körs varje gång du pushar — och berättar om något gick fel.

## Skapa filen

```bash
mkdir -p .github/workflows
```

Skapa `.github/workflows/ci.yml`:

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Hämta koden
        uses: actions/checkout@v4

      - name: Säg hej
        run: echo "Workflow igång!"
```

Committa och pusha. Gå till fliken **Actions** på GitHub — du ser workflow:en köra i realtid.

## Vad varje del gör

```yaml
name: CI
```
Visningsnamnet i GitHub-gränssnittet.

```yaml
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
```
Kör vid push till `main` och vid PR mot `main`.

```yaml
runs-on: ubuntu-latest
```
Kör på en Linux-maskin som GitHub tillhandahåller. Alternativ: `windows-latest`, `macos-latest`.

```yaml
- uses: actions/checkout@v4
```
Hämtar koden från repot till runner-maskinen. Utan det här steget finns inga filer att jobba med.

```yaml
- run: echo "Workflow igång!"
```
Kör ett vanligt shell-kommando. `run` kan köra vad som helst — kommandon, skript, CLI-verktyg.

## Gröna bockar och röda kryss

Om alla steg lyckas: grön bock på committen i GitHub.
Om ett steg misslyckas (exit code ≠ 0): rött kryss — och du får ett mejl.

Det är hela poängen: du behöver inte komma ihåg att köra testerna. GitHub påminner dig om du glömmer.

## Nästa steg

Det här är skelettet. Lägg till steg för kompilering och testning — se [Kompilera och testa C#](csharp-ci.md).
