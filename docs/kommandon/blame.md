---
title: git blame
description: "Se vem som senast ändrade varje rad i en fil — och i vilken commit."
parent: Kommandon
nav_order: 160
---

# git blame

Se vem som senast ändrade varje rad i en fil — och i vilken commit.

Trots namnet är det inte ett anklagelsverktyg. Det heter "blame" av historiska skäl. I praktiken används det för att förstå **varför** en rad ser ut som den gör, och vem man kan fråga om man inte förstår.

```bash
git blame Kassan.cs
```

```plaintext
a3f8c21 (Pelle Persson  2026-09-14 10:23) public decimal BeraknaTotal()
9d2e1f0 (Anna Lindgren  2026-09-12 14:05) {
9d2e1f0 (Anna Lindgren  2026-09-12 14:05)     var total = produkter.Sum(p => p.Pris);
a3f8c21 (Pelle Persson  2026-09-14 10:23)     if (rabattkod != null)
a3f8c21 (Pelle Persson  2026-09-14 10:23)         total -= rabattkod.BeraknaRabatt(total);
9d2e1f0 (Anna Lindgren  2026-09-12 14:05)     return total;
9d2e1f0 (Anna Lindgren  2026-09-12 14:05) }
```

Varje rad: commit-hash · författare · datum · radinnehåll.

## Undersöka en specifik commit

Ser du en commit-hash du vill veta mer om?

```bash
git show a3f8c21
```

Visar hela committen — meddelande, diff, alla filer som ändrades. Nu vet du inte bara **vem** som ändrade raden utan också **varför** (förutsatt att commit-meddelandet är vetigt).

## Begränsa till ett radintervall

```bash
git blame -L 10,25 Kassan.cs     # bara rad 10–25
git blame -L 10,+15 Kassan.cs    # rad 10 och 15 rader framåt
```

## Ignorera whitespace-ändringar

```bash
git blame -w Kassan.cs
```

Bra om en kollega formaterat om hela filen — utan `-w` pekar blame på formateringscommitsen istället för den egentliga ändringen.

## I VS Code

Du behöver inte alltid terminalen. VS Code (och de flesta git-klienter) visar blame inline bredvid koden när du håller muspekaren på en rad, eller via `Git: Toggle File Blame` i kommandopaletten.
