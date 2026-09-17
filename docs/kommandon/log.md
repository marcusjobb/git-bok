---
title: git log
parent: Kommandon
nav_order: 60
---

# git log

Bläddra i projektets historik. `git log` i sin grundform spottar ut alla commits med hash, författare, datum och meddelande — troligtvis mer än du behöver se.

```bash
git log
```

```plaintext
commit a3f8c21d4e9b7f2a1c0d5e8f3b6a9c2d4e7f1b0a
Author: Pelle Persson <pelle@example.com>
Date:   Thu Sep 14 10:23:45 2026 +0200

    feat: lägg till rabattkod-validering i kassan
```

## Användbara flaggor

```bash
git log --oneline           # en rad per commit — mycket mer skanbart
git log --oneline --graph   # + visuellt träd över branches och merges
git log -5                  # bara de senaste fem commitsen
git log --author="Pelle"    # bara Pelles commits
git log --since="2 weeks ago"
git log --until="2026-09-01"
git log -- Kassan.cs        # bara commits som rört den här filen
```

## Hitta vad som ändrats i en specifik commit

```bash
git show a3f8c21                # visa diffsen för den committen
git show a3f8c21:Kassan.cs      # visa filen som den såg ut i den committen
```

Du behöver inte skriva hela hash-strängen — de första 7 tecknen räcker nästan alltid.

## Söka i commit-meddelanden

```bash
git log --grep="rabattkod"      # commits vars meddelande innehåller "rabattkod"
git log -S "VisaFelmeddelande"  # commits som lade till eller tog bort den textsträngen i koden
```

`-S` (kallas "pickaxe") är ovärderlig när du vill veta **när** en specifik funktion eller variabel dök upp — eller försvann.

## En bra standardalias

De flesta lägger till det här i sin git-config:

```bash
git config --global alias.lg "log --oneline --graph --decorate --all"
```

Sedan räcker det med:

```bash
git lg
```

```plaintext
* a3f8c21 (HEAD -> feature/rabattkod) feat: lägg till rabattkod-validering
* 9d2e1f0 (main) fix: förhindra krasch när kundvagnen är tom
* 7b4a3c8 feat: lägg till kundvagn
```
