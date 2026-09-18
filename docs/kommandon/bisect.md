---
title: git bisect
description: "git bisect i Kommandon — Git-boken av Marcus Ackre Medina"
parent: Kommandon
nav_order: 170
---

# git bisect

Hitta exakt vilken commit som introducerade en bugg — utan att manuellt testa hundra commits.

`git bisect` gör en binärsökning i historiken. Du talar om för Git "det fungerade i commit X, det är trasigt nu" — sedan testar den commits halvvägs och frågar om det fungerar eller inte. Processen halverar antalet möjliga kandidater varje steg. 100 commits → 7 steg.

## Starta en bisect-session

```bash
git bisect start
git bisect bad                    # nuvarande commit är trasig
git bisect good v1.0              # den här versionen fungerade
```

Git checkar nu ut en commit halvvägs i historiken. Testa manuellt, rapportera resultatet:

```bash
git bisect good    # den här är OK — buggen kom senare
git bisect bad     # den här är trasig — buggen kom tidigare
```

Upprepa. Efter ett antal steg:

```plaintext
a3f8c21 is the first bad commit
Author: Pelle Persson <pelle@example.com>
Date:   Thu Sep 14 10:23:45 2026

    feat: lägg till rabattkod-validering i kassan
```

Nu vet du var buggen introducerades. Läs committen med `git show a3f8c21`.

## Avsluta

```bash
git bisect reset    # återgår till HEAD, sessionen rensas
```

Glöm inte att köra det här — annars är du kvar i "detached HEAD"-läge.

## Automatiserad bisect

Om du har ett test som returnerar 0 vid framgång och 1 vid fel kan du automatisera hela processen:

```bash
git bisect start
git bisect bad
git bisect good v1.0
git bisect run dotnet test --filter "TestRabattkod"
```

Git kör testet automatiskt för varje kandidat och hittar den buggiga committen utan att du behöver göra något.

## Praktiskt scenario

Du deployade igår kväll och allt fungerade. Idag är kassan trasig. Historiken har 80 commits sedan igårkvällens deploy:

```bash
git bisect start
git bisect bad HEAD
git bisect good deploy-2026-09-16
```

Sju frågor från Git senare vet du exakt vilken commit som förstörde det.
