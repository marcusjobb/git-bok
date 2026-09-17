---
title: Git
layout: default
parent: Ordlista
nav_order: 10
---
## Git

| Ord | Förklaring |
| --- | --- |
| Branch | En gren i repot — en parallell version av koden. |
| Cherry-pick | Att plocka in en specifik commit från en annan branch, utan att mergea hela branchen. |
| Checkout | Att byta gren, eller (äldre syntax) återställa filer till ett tidigare tillstånd. |
| Clone | Att kopiera ett repo till din dator, med hela historiken. |
| Commit | En sparad ögonblicksbild av projektet vid en specifik tidpunkt. |
| Feature branch | En tillfällig branch för en avgränsad funktion, grenad ut från huvudgrenen och mergad tillbaka när den är klar. |
| Feature flag | Ett villkor i koden som slår av/på en funktion utan att kräva en ny deploy — gör det möjligt att committa ofärdig kod till main utan att visa den för användarna. |
| Fork | Din personliga kopia av någon annans repo på GitHub. |
| Git | Ett versionshanteringssystem — håller koll på varje ändring i koden över tid. |
| Git Flow | Branching-strategi med fem branch-typer (main, develop, feature, release, hotfix) — passar schemalagda releaser. |
| GitHub Flow | Enklare branching-strategi — en huvudgren (main) och korta feature branches, allt mergas via Pull Request. |
| .gitignore | En fil som talar om för Git vilka filer som aldrig ska sparas i historiken. |
| git add | Flyttar en ändring från Working Directory till Staging Area. |
| git init | Förvandlar en vanlig mapp till ett Git-repo. |
| git status | Visar vad som ändrats sedan senaste commit. |
| Hotfix branch | En akut fix som grenas direkt från produktionsgrenen och mergas tillbaka till både produktion och utvecklingsgrenen. |
| Merge | Att slå ihop två grenar. |
| Merge-konflikt | När Git inte kan slå ihop två versioner av samma fil automatiskt, för att samma rad ändrats på två håll. |
| Origin | Det vanligaste namnet på en remote. |
| Pull | Att hämta ner ändringar från fjärrrepot. |
| Pull Request (PR) | En förfrågan att mergea en branch till en annan, med möjlighet för teamet att granska koden först. GitHubs funktion, inte Gits. |
| Push | Att skicka upp ändringar till fjärrrepot. |
| Rebase | Att flytta en gren till en ny startpunkt genom att spela av dess commits ovanpå en annan gren. |
| Release branch | En tillfällig branch i Git Flow för sista finputsningen innan en release går till produktionsgrenen. |
| Remote | En koppling till ett annat repo, oftast på GitHub. |
| Repository | Mappen som innehåller alla filer och hela ändringshistoriken för ett projekt. |
| Squash | Att slå ihop flera commits till en enda innan de mergas — gör historiken renare. |
| SSH-nyckel | Ett nyckelpar (privat + publik) som låter dig ansluta till GitHub utan att skriva lösenord varje gång. |
| Stash | Att spara undan ändringar som inte är klara, utan att committa dem. |
| Staging Area | Förberedelseplatsen mellan Working Directory och Repository — `git add` flyttar en fil hit. |
| Tag | En namngiven markering av en specifik commit, oftast använd för versionsnummer (t.ex. `v1.1`). |
| Trunk-based development | Branching-strategi där nästan alla commits går direkt till huvudgrenen, i små steg, ofta bakom feature flags. |
| Upstream | Det vanligaste namnet på en remote som inte är din egen — t.ex. originalrepot du forkat från. |
| Working Directory | Mappen där du faktiskt kodar och redigerar filer. |
