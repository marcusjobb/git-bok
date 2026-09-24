---
title: Kompilera och testa C#
description: "En komplett CI-pipeline för ett .NET-projekt — kompilerar och kör tester vid varje push och PR."
parent: GitHub Actions
nav_order: 30
---

# Kompilera och testa C#

En komplett CI-pipeline för ett .NET-projekt — kompilerar och kör tester vid varje push och PR.

## Workflow-filen

`.github/workflows/ci.yml`:

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
      - name: Hämta koden
        uses: actions/checkout@v4

      - name: Installera .NET
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '9.0.x'

      - name: Återställ beroenden
        run: dotnet restore

      - name: Kompilera
        run: dotnet build --no-restore --configuration Release

      - name: Kör tester
        run: dotnet test --no-build --configuration Release --verbosity normal
```

Committa filen och pusha. Fliken **Actions** på GitHub visar varje steg i realtid.

## Vad varje steg gör

**`actions/checkout@v4`** — hämtar repots kod till runner-maskinen.

**`actions/setup-dotnet@v4`** — installerar angiven .NET-version. `9.0.x` matchar den senaste patch-versionen av .NET 9.

**`dotnet restore`** — laddar ner NuGet-paket. Måste köras innan build.

**`dotnet build --no-restore`** — kompilerar projektet. `--no-restore` hoppar över att ladda ner paket igen (vi gjorde det i föregående steg). `--configuration Release` bygger i Release-läge, inte Debug.

**`dotnet test --no-build`** — kör alla testprojekt i solutionen. `--no-build` hoppar över kompilering (redan gjort). Om ett test misslyckas returnerar kommandot exit code 1 — steget markeras rött, workflow:en misslyckas, du får ett mejl.

## Flera .NET-versioner

Vill du testa att projektet fungerar på både .NET 8 och .NET 9?

```yaml
jobs:
  build-and-test:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        dotnet-version: ['8.0.x', '9.0.x']

    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-dotnet@v4
        with:
          dotnet-version: ${{ matrix.dotnet-version }}

      - run: dotnet restore
      - run: dotnet build --no-restore --configuration Release
      - run: dotnet test --no-build --configuration Release
```

GitHub kör nu två parallella jobb — ett per .NET-version. Bra sätt att fånga kompatibilitetsproblem tidigt.

## Cacha NuGet-paket

`dotnet restore` laddar ner paket varje gång. Det tar tid. Lägg till caching:

```yaml
      - name: Cacha NuGet-paket
        uses: actions/cache@v4
        with:
          path: ~/.nuget/packages
          key: nuget-${{ hashFiles('**/*.csproj') }}
          restore-keys: nuget-
```

Lägg det här steget **före** `dotnet restore`. Nästa körning hittar paketen i cache — några sekunder istället för tiotals sekunder.

## Tolka resultatet

| Status | Betyder |
|--------|---------|
| ✅ Grön bock | Kompilerar och alla tester gröna |
| ❌ Rött kryss på "Kompilera" | Kompileringsfel — din kod bygger inte |
| ❌ Rött kryss på "Kör tester" | Tester misslyckas — koden bygger men beter sig fel |

Klicka på det röda krysset i GitHub → Actions → jobbet → det specifika steget för att se exakt vilket fel som uppstod.
