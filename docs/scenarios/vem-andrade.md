---
title: Vem ändrade vad och när
description: "Vem ändrade vad och när i Scenarios — Git-boken av Marcus Ackre Medina"
parent: Scenarios
nav_order: 60
---

# Vem ändrade vad och när

Något är trasigt. Du vet inte sedan när, och du vet inte vem som rörde det. Det här är detektivarbete — och Git har verktygen.

## Steg 1: Hitta den skyldiga raden — git blame

```bash
git blame Kassan.cs
```

```plaintext
a3f8c21 (Pelle Persson  2026-09-14) public decimal BeraknaTotal()
a3f8c21 (Pelle Persson  2026-09-14)     var total = produkter.Sum(p => p.Pris);
b7c3d2e (Anna Lindgren  2026-09-10)     if (produkter == null) return 0;
```

Varje rad: commit · vem · när. Du ser direkt om det är Pellas refaktorering den 14:e eller Annas null-check den 10:e som är problemet.

Vill du bara titta på ett specifikt område:

```bash
git blame -L 45,60 Kassan.cs
```

## Steg 2: Förstå committen — git show

Hittade du en misstänkt commit-hash? Kolla vad den faktiskt gjorde:

```bash
git show a3f8c21
```

Visar commit-meddelande, författare, datum, och exakt diff. Nu vet du inte bara **vem** som ändrade raden utan **varför** — förutsatt att commit-meddelandet är informativt.

## Steg 3: Hitta när en funktion försvann — git log -S

`-S` (pickaxe) söker i historiken efter commits som lade till eller tog bort en specifik textsträng:

```bash
git log -S "BeraknaRabatt" --oneline
```

```plaintext
a3f8c21 feat: lägg till rabattkod-validering
f2e1d0c refactor: byt namn på BeraknaTotal
```

Bra när du vet att en funktion *funnits* men inte längre finns — eller när du vill se alla commits som rört en specifik metod.

## Steg 4: Hitta den exakta buggy committen — git bisect

Du vet att det fungerade i fredags och är trasigt idag. Det är 40 commits sedan fredag.

```bash
git bisect start
git bisect bad                      # nu är det trasigt
git bisect good v2026-09-12         # fredag, fungerade
```

Git checkar ut en commit halvvägs i historiken. Testa. Rapportera:

```bash
git bisect good    # fungerar — buggen kom efter det här
git bisect bad     # trasigt — buggen kom innan det här
```

Fem till sex steg senare:

```plaintext
a3f8c21 is the first bad commit

    feat: lägg till rabattkod-validering i kassan

    +    if (rabattkod != null)
    +        total -= rabattkod.BeraknaRabatt(total);
```

Bingo. Avsluta:

```bash
git bisect reset
```

## Kombinera allt

Praktiskt flöde när du hittar en bugg utan att veta vem eller när:

```
git blame → hitta misstänkt rad och commit-hash
    ↓
git show <hash> → förstå vad committen faktiskt gjorde
    ↓
git log -S "<nyckelord>" → se alla commits som rört det området
    ↓
git bisect → om du fortfarande inte hittat det, binärsök historiken
```

Den skyldiga committen är i princip alltid hittbar. Git har hela historiken — det handlar bara om att ställa rätt frågor.
