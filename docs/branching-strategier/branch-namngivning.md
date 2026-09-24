---
title: Branch-namngivning
description: "En branch är ett löfte till teamet: \"det här jobbar jag på just nu.\" Bra namn håller det löftet. Dåliga namn är ett slag i luften."
parent: Branching-strategier
nav_order: 5
---

# Branch-namngivning

En branch är ett löfte till teamet: _"det här jobbar jag på just nu."_ Bra namn håller det löftet. Dåliga namn är ett slag i luften.

## Typen först

Sätt alltid en prefix som talar om **vad** branchen är till för:

| Prefix      | Används när                                                     |
| ----------- | --------------------------------------------------------------- |
| `feature/`  | Du bygger något nytt                                            |
| `fix/`      | Du rättar en bugg                                               |
| `hotfix/`   | Akut fix direkt mot produktion (Git Flow)                       |
| `chore/`    | Uppdatering som inte påverkar användaren (beroenden, CI-config) |
| `docs/`     | Bara dokumentationsändringar                                    |
| `refactor/` | Omstrukturering utan nytt beteende                              |

## Sedan — vad handlar det om?

```bash
# Bra
feature/kundvagn-rabattkod
fix/kassan-kraschar-vid-tom-kundvagn
chore/uppdatera-dotnet-8
docs/lagg-till-api-exempel

# Dåliga
feature/ny-grej
fix/bug
johns-branch
test123
wip
hej
```

`wip` (work in progress) som branch-namn är en välkänd varningssignal. Det berättar ingenting och ger en obehaglig känsla av att ingen vet när branchen är klar — för det vet troligtvis inte ens skaparen.

## Håll det kort och skanbart

Tre till fem ord räcker nästan alltid. Använd bindestreck, aldrig underscore eller camelCase — det är en URL, inte en variabel.

```bash
# Bra
fix/inloggning-misslyckas-med-specialtecken

# Onödigt lång
fix/anvandarinloggning-kastar-exception-nar-losenordet-innehaller-specialtecken-som-utropstecken

# Svårläst
fix/inloggningMislyckasMedSpecialtecken
fix/inloggning_misslyckas_med_specialtecken
```

## Koppling till uppgiftssystem

Om teamet använder GitHub Issues, Jira, eller Linear — lägg till ticket-numret. Det gör det trivialt att hoppa mellan kod och kontext:

```bash
feature/42-kundvagn-rabattkod
fix/gh-137-kassan-kraschar
```

GitHub känner igen `gh-137` och länkar automatiskt till issue #137 i Pull Requesten.

## Commit-meddelanden hänger ihop med branch-namn

Branchen är rubriken. Commitsen är innehållsförteckningen. Om de berättar samma historia är det enklare för nästa person (eller du själv om tre månader) att förstå vad som hände:

```bash
# Branch: feature/kundvagn-rabattkod

git commit -m "feat: lägg till rabattkods-input i kundvagnsvyn"
git commit -m "feat: validera koden mot API vid checkout"
git commit -m "fix: visa felmeddelande om koden är utgången"
```

Det här mönstret — `typ: kort beskrivning` — kallas **Conventional Commits** och är standard i de flesta moderna projekt. Det gör det möjligt att generera en `CHANGELOG.md` automatiskt, och GitHub Actions kan använda det för att automatiskt sätta versionsnummer.

```
feat:     ny funktion (minor version bump)
fix:      buggfix (patch version bump)
docs:     dokumentation
chore:    inget som påverkar användaren
refactor: omstrukturering
test:     lägga till eller ändra tester
```
