---
title: Testa dig själv
description: "Du behöver ett riktigt GitHub-repo för det här — det går inte att simulera lokalt. Skapa ett testmiljö-repo på GitHub om du inte redan har ett."
parent: GitHub Actions
nav_order: 999
---

# Testa dig själv — GitHub Actions

Du behöver ett riktigt GitHub-repo för det här — det går inte att simulera lokalt. Skapa ett testmiljö-repo på GitHub om du inte redan har ett.

---

## Del 1 — Skapa din första workflow

Skapa en workflow-fil i ditt testmiljö-repo:

```bash
mkdir -p .github/workflows
```

Skriv en workflow som:
- Triggar på varje push till `main`
- Kör på `ubuntu-latest`
- Har ett enda steg: kör `echo "Hej från Actions!"`

Pusha och kontrollera att fliken **Actions** på GitHub visar en grön körning.

---

## Del 2 — Fånga ett avsiktligt fel

Ändra workflow:en så att ett steg avsiktligt misslyckas:

```yaml
- name: Misslyckas med flit
  run: exit 1
```

Pusha. Vad händer i GitHub Actions-fliken? Vilken status visas på committen i listan?

Återställ sedan workflow:en till ett fungerande tillstånd.

---

## Del 3 — C# CI i praktiken

Om du har ett .NET-projekt (eller skapar ett nytt med `dotnet new console`):

1. Skapa workflow-filen från [Kompilera och testa C#](csharp-ci.md)
2. Pusha
3. Gå till Actions och följ körningen steg för steg
4. Introducera ett kompileringsfel i koden och pusha — vad händer?
5. Fixa felet och pusha igen

---

## Del 4 — Läs ett misslyckat Actions-resultat

Hitta en röd körning i Actions (antingen din från Del 2, eller sök bland dina repos). Klicka dig in till det röda steget.

Besvara:
1. Vilket steg misslyckades?
2. Vad stod det i loggen?
3. Vilken exit-kod returnerade det?

---

## Quiz — Sant eller falskt?

1. En workflow triggas alltid när du pushar, oavsett vad `on:` säger.
2. `actions/checkout@v4` laddar ner ditt repo till runner-maskinen.
3. Om ett steg i ett job misslyckas fortsätter nästa steg i samma job automatiskt.
4. Du kan ha flera jobs i samma workflow-fil.
5. `dotnet test --no-build` förutsätter att projektet redan är byggt i ett tidigare steg.
6. GitHub Actions är gratis utan begränsning för privata repos.

---

## Bonusutmaning

Lägg till ett `on: pull_request`-trigger till din CI-workflow. Skapa sedan en branch, gör en ändring, och öppna en PR.

Vad ser du i PR:en på GitHub? Var visas Actions-resultatet?
