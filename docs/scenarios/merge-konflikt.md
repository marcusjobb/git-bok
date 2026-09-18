---
title: Lösa en merge-konflikt
description: "Lösa en merge-konflikt i Scenarios — Git-boken av Marcus Ackre Medina"
parent: Scenarios
nav_order: 40
---

# Lösa en merge-konflikt

Git klarar de flesta mergar automatiskt. Men när samma rad ändrats på två ställen kan den inte gissa vilket som är rätt — det är upp till dig.

Det ser skrämmande ut första gången. Det är inte farligt.

## Vad som händer

Du kör `git merge` eller `git pull` och får:

```plaintext
Auto-merging Kassan.cs
CONFLICT (content): Merge conflict in Kassan.cs
Automatic merge failed; fix conflicts and then commit the result.
```

Git har pausat. Inget är förstört — Git väntar bara på ett beslut.

## Hitta alla konflikter

```bash
git status
```

```plaintext
Unmerged paths:
  both modified:   Kassan.cs
```

Öppna filen. Konflikten ser ut såhär:

```csharp
<<<<<<< HEAD
    var total = produkter.Sum(p => p.Pris * 0.9m);  // 10% kampanjrabatt
=======
    var total = produkter.Sum(p => p.Pris);
    if (rabattkod != null)
        total -= rabattkod.BeraknaRabatt(total);
>>>>>>> feature/rabattkod
```

- `<<<<<<< HEAD` till `=======` — din version (branchen du är på)
- `=======` till `>>>>>>>` — den inkommande versionen (branchen du mergade in)

## Lös konflikten

Bestäm vad den slutliga koden ska vara. Ta bort konfliktmarkeringarna (`<<<<<<<`, `=======`, `>>>>>>>`) och skriv rätt kod. Ofta är svaret att kombinera båda:

```csharp
    var total = produkter.Sum(p => p.Pris);
    if (rabattkod != null)
        total -= rabattkod.BeraknaRabatt(total);
    // kampanjrabatter hanteras via rabattkod-systemet nu
```

## Avsluta

```bash
git add Kassan.cs        # markera konflikten som löst
git commit               # Git föreslår ett merge-commit-meddelande
```

Är det flera filer med konflikter: lös dem en i taget, `git add` var och en, sedan ett enda `git commit` på slutet.

## Avbryta om du ångrar dig

Vill du backa och börja om?

```bash
git merge --abort
```

Återgår till exakt läget innan du startade mergen.

## I VS Code

VS Code har inbyggt stöd för merge-konflikter. Det visar `Accept Current Change`, `Accept Incoming Change`, `Accept Both Changes` direkt i editorn bredvid konfliktmarkeringarna. Enklare än att redigera markeringarna manuellt.

## Tips: minska konflikter i framtiden

Konflikter uppstår när branches lever länge och divergerar. Mergea (eller rebasea) `main` till din feature-branch regelbundet — hellre många små konflikter längs vägen än en stor i slutet.
