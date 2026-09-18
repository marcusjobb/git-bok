---
title: git diff
description: "git diff i Kommandon — Git-boken av Marcus Ackre Medina"
parent: Kommandon
nav_order: 70
---

# git diff

Visa exakt vilka rader som ändrats — innan du committar, eller mellan commits.

```bash
git diff
```

Utan argument visar det skillnaden mellan working directory och staging area — alltså **ändringar du gjort men inte stagat**.

## De tre lägena

```bash
git diff                        # working directory vs staging area
git diff --staged               # staging area vs senaste commit (vad som faktiskt committas)
git diff main..feature/rabattkod  # jämför två branches
git diff a3f8c21..9d2e1f0       # jämför två specifika commits
```

`git diff --staged` är det viktiga innan en commit — det är exakt det som kommer att sparas.

## Läsa en diff

```diff
@@ -12,6 +12,10 @@ public decimal BerakhnaTotal()
-    return produkter.Sum(p => p.Pris);
+    var total = produkter.Sum(p => p.Pris);
+    if (rabattkod != null)
+        total -= rabattkod.BerakhnaRabatt(total);
+    return total;
```

- `@@` visar var i filen ändringen är (rad 12, 6 rader gamla, 10 rader nya)
- `-` (röd) = rad som tagits bort
- `+` (grön) = rad som lagts till

## En specifik fil

```bash
git diff Kassan.cs
git diff --staged Kassan.cs
```

## Statistik utan detaljerna

```bash
git diff --stat
```

```plaintext
 Kassan.cs | 8 +++++---
 Program.cs | 2 +-
 2 files changed, 7 insertions(+), 3 deletions(-)
```

Bra för att snabbt se hur stor en ändring är utan att läsa varje rad.
