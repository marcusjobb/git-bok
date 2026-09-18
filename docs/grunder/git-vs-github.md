---
title: Git ≠ GitHub
description: "Git ≠ GitHub i Grunder — Git-boken av Marcus Ackre Medina"
parent: Grunder
nav_order: 5
---

# Git ≠ GitHub

Det här är förmodligen den vanligaste förvirringen bland nybörjare — och den är helt förståelig, eftersom namnen är så lika. Men de är två helt olika saker.

## Git

**Git** är ett program du installerar på din dator. Det håller koll på ändringar i filer, låter dig skapa branches, och sparar hela historiken lokalt.

Git uppfanns av Linus Torvalds 2005 — samma person som skapade Linux-kärnan. Han behövde ett bra versionshanteringssystem för att koordinera tusentals bidragsgivare till Linux. Inga moln. Ingen webbplats. Bara ett program som körs på din dator.

```bash
git init        # Git vet ingenting om internet
git add .       # allt detta händer lokalt
git commit -m "Initial commit"
```

Du kan använda Git helt utan internet, utan ett konto någonstans, utan GitHub. Git funkar utmärkt för ett projekt som bara du jobbar på, lokalt på din dator.

## GitHub

**GitHub** är en webbplats — en tjänst som låter dig lagra ditt Git-repo online och samarbeta med andra.

GitHub tillhör Microsoft (köptes 2018). Tanken är enkel: eftersom Git redan håller koll på allt och kan synka mot ett fjärrrepo — varför inte bygga en snygg webbplats som hostar det fjärrrepot?

GitHub lade till Pull Requests, issues, projekt-tavlor, Actions, och mycket annat ovanpå Git. Men allt det är Githubs egna funktioner — inte en del av Git.

## Analogin

> Git är som ett Word-dokument med versionshistorik.
> GitHub är som OneDrive — platsen du lagrar det och delar det med andra.

Dokumentet funkar utan OneDrive. OneDrive är meningslöst utan något att lagra.

## Andra plattformar gör samma sak

GitHub är den absolut vanligaste, men det finns alternativ — alla använder Git under huven:

| Plattform | Ägs av | Nisch |
|-----------|--------|-------|
| **GitHub** | Microsoft | Störst, mest open source |
| **GitLab** | GitLab Inc. | Kan self-hostas, inbyggd CI/CD |
| **Codeberg** | Ideell förening | EU-baserad, ingen tracking |
| **Azure DevOps** | Microsoft | Företagsvärlden, Microsoftekosystemet |
| **Bitbucket** | Atlassian | Jira-integration |

Lär du dig Git fungerar du med alla av dem.

## Varför spelar det roll?

När något inte fungerar är det skillnad på att felsöka ett Git-problem och ett GitHub-problem:

- `git push` misslyckas? Kan vara ett SSH-nyckel-problem (Git + GitHub-konfiguration).
- Pull Requesten syns inte? Det är ett GitHub-problem — ingenting med Git att göra.
- `git merge` skapar en konflikt? Rent Git — GitHub är inte inblandat.

Vet du vilken del av stacken problemet sitter i, vet du också var du ska leta efter lösningen.
