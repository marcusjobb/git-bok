---
title: .gitignore
description: ".gitignore i Grunder — Git-boken av Marcus Ackre Medina"
parent: Grunder
nav_order: 30
---

# .gitignore

Git trackar allt — om du inte säger åt det att sluta.

En `.gitignore`-fil är en lista med filer och mappar som Git ska blunda för. Det låter enkelt. Men konsekvenserna av att missa den är allt annat än enkla.

---

## Varför det spelar roll

Utan `.gitignore` hamnar följande i ditt repo — och på GitHub:

- **Lösenord och API-nycklar** i `.env` och `appsettings.json`
- **Kompilerade filer** i `bin/` och `obj/` — stora, onödiga, genereras om automatiskt
- **IDE-inställningar** i `.vs/` och `.idea/` — stör kollegor som använder en annan editor
- **Beroenden** i `node_modules/` — kan väga gigabytes, installeras med ett kommando

Ett råkat pushat lösenord är inte bara pinsamt. Bots skannar GitHub konstant och hittar nycklar inom sekunder. Se [Råkade commita secrets](../scenarios/commitat-secrets.md) för vad du gör om det händer.

---

## Syntax

```plaintext
# Kommentar — ignoreras av Git

bin/              # hela mappen
*.dll             # alla filer med .dll-ändelse
!important.dll    # men inte den här — undantag med !

.env              # en specifik fil
.env.*            # alla varianter: .env.local, .env.production...

# Mapp var som helst i repot
**/logs/

# Bara i roten
/secrets.json
```

**`*`** matchar vad som helst utom `/`  
**`**`** matchar vad som helst inklusive `/` (dvs. alla nivåer)  
**`!`** är ett undantag — inkludera trots att ett tidigare mönster utesluter

---

## .gitignore för C# / .NET

```plaintext
# Kompilerat
bin/
obj/

# Visual Studio
.vs/
*.user
*.suo

# Rider / JetBrains
.idea/

# Känslig konfiguration
appsettings.*.json
!appsettings.json
*.env
.env
secrets.json
```

`appsettings.*.json` fångar `appsettings.Development.json`, `appsettings.Production.json` m.fl. — men `!appsettings.json` (utan miljösuffix) tillåts ändå, eftersom den brukar innehålla ofarliga standardvärden.

---

## Generera en .gitignore automatiskt

Istället för att skriva den för hand — använd [gitignore.io](http://gitignore.io/).

Välj ditt språk, ramverk och IDE. Kopiera resultatet till `.gitignore` i rotkatalogen.

```bash
# Eller via curl direkt i terminalen:
curl -o .gitignore https://www.toptal.com/developers/gitignore/api/csharp,visualstudio,rider
```

---

## Lägg till .gitignore tidigt

`.gitignore` ska vara **första eller andra committen** i ett nytt repo — inte något du lägger till "sen".

Varför? Filer som redan är trackade ignoreras inte av `.gitignore`, även om du lägger till dem efteråt. Du måste aktivt berätta för Git att sluta tracka dem:

```bash
git rm --cached appsettings.Development.json
git add .gitignore
git commit -m "chore: sluta tracka känslig konfigurationsfil"
```

`--cached` tar bort filen från Git men behåller den lokalt på disken.

---

## Global .gitignore

Vill du aldrig råka commita `.DS_Store` (Mac) eller `Thumbs.db` (Windows)? Skapa en global `.gitignore` som gäller alla dina repos:

```bash
git config --global core.excludesfile ~/.gitignore_global
```

Lägg sedan in dina OS- och editor-specifika mönster i `~/.gitignore_global` en gång — slipper upprepa dem i varje repo.
