---
title: git add
description: "Flytta ändringar från working directory till staging area. Du bestämmer exakt vad som ska ingå i nästa commit."
parent: Kommandon
nav_order: 20
---

# git add

```mermaid
flowchart LR
    WD["**Working Directory**"]
    ST["Stash"]
    SA["**Staging Area**"]
    LR["Local Repository"]
    RE[("Remote\n(GitHub)")]

    WD <-->|stash / pop| ST
    WD -->|git add| SA
    SA -->|git commit| LR
    LR -->|git push| RE
    RE -->|git fetch| LR
    LR -.->|git merge| WD

    style WD fill:#1565c0,stroke:#0d47a1,color:#fff
    style SA fill:#1565c0,stroke:#0d47a1,color:#fff
```

Flytta ändringar från working directory till staging area. Du bestämmer exakt vad som ska ingå i nästa commit.

```bash
git add filnamn.cs          # en specifik fil
git add src/                # hela mappen
git add .                   # allt som ändrats
git add -p                  # interaktivt — välj rad för rad
```

## Varför inte alltid `git add .`?

`git add .` tar **allt** — inklusive filer du inte menat att committa. En temporär testfil, ett lösenord du glömt i `appsettings.json`, en halvfärdig klass du inte är klar med.

Vana att bygga: `git status` → `git add <specifika filer>` → `git status igen` → `git commit`.

## Interaktivt läge — `git add -p`

Det mäktigaste sättet att staga. Istället för att staga hela filer kan du välja **vilka rader** i en fil som ska ingå i committen:

```bash
git add -p Program.cs
```

```plaintext
@@ -12,6 +12,10 @@ public class Program
     Console.WriteLine("Hej!");
+    // TODO: ta bort debug-logg
+    Console.WriteLine(rabattkod);
+
     return 0;
```

```plaintext
Stage this hunk [y,n,q,a,d,s,?]?
```

`y` = staga det här blocket. `n` = hoppa över. `s` = dela upp i ännu mindre bitar.

Bra när du gjort flera orelaterade ändringar i samma fil och vill committa dem separat — en tydlig commit-historik är värd det lilla extra jobbet.

## Unstaga en fil

Stagat fel fil? Ingen fara:

```bash
git restore --staged Kassan.cs
```

Filen går tillbaka till "changed but not staged". Ingenting i working directory påverkas.
