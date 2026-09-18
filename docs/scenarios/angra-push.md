---
title: Ångra en push
description: "Ångra en push i Scenarios — Git-boken av Marcus Ackre Medina"
parent: Scenarios
nav_order: 20
---

# Ångra en push

Du pushade och insåg direkt efteråt att något var fel. Kanske fel branch, kanske halvfärdig kod, kanske ett commit-meddelande som inte borde ha gått ut.

Det finns inte ett säkert sätt att ta bort något från en delad remote. Men det finns sätt att hantera det.

## Alternativ 1: git revert — det säkra alternativet

Skapar en ny commit som gör det omvända av den du pushade. Historiken förblir intakt — det syns att något angrades, men ingen historik skrivs om.

```bash
git revert a3f8c21   # hash på committen du vill ångra
git push
```

Bra om andra kan ha hämtat din push redan. Deras historik fungerar fortfarande.

## Alternativ 2: git push --force-with-lease — om ingen hunnit hämta

Om du pushade för några sekunder sedan och du är säker på att ingen hunnit `git pull`:

```bash
git reset HEAD~1          # ta bort senaste committen lokalt
# fixa vad som behöver fixas
git commit -m "rätt commit-meddelande"
git push --force-with-lease
```

`--force-with-lease` vägrar om remote har commits du inte har lokalt — ett säkerhetsnät mot att skriva över andras arbete.

**Kör aldrig `--force` (utan `-with-lease`) på en delad branch.**

## Alternativ 3: Fel branch — flytta och rensa

Pushade du till `main` men menade `feature/rabattkod`?

```bash
# Skapa feature-branchen från din nuvarande position
git switch -c feature/rabattkod
git push -u origin feature/rabattkod

# Revert på main
git switch main
git revert a3f8c21
git push
```

## Vad väljer man?

| Situation | Välj |
|-----------|------|
| Ingen hunnit hämta, du är snabb | `reset` + `push --force-with-lease` |
| Osäker på om någon hämtat | `git revert` |
| Pushade secrets | Se [Råkade commita secrets](commitat-secrets.md) |
| Pushade till fel branch | Skapa rätt branch + `revert` på fel branch |

Grundregeln: om det finns minsta risk att någon hunnit hämta — `revert`. Det är alltid det säkrare valet.
