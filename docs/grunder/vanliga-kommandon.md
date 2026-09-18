---
title: Vanliga kommandon
description: "Vanliga kommandon i Grunder — Git-boken av Marcus Ackre Medina"
parent: Grunder
nav_order: 20
---

# Vanliga kommandon

## git status — kolla läget innan du gör något

Det kommandot du ska köra **innan** du gör något annat. Det visar exakt vad som ändrats sedan senaste commit.

```bash
git status
```

```plaintext
On branch main
Changes not staged for commit:
  modified:   Program.cs
```

**Ritualen:** `git status` → `git add` → `git commit` → `git push`. Varje gång. Det blir en ryggmärgsreflex efter ett par veckor.

```mermaid
flowchart TD
    A[git status] --> B{Något ändrat?}
    B -->|Ja| C[git add]
    B -->|Nej| F[Klart, inget att göra]
    C --> D[git commit -m '...']
    D --> E[git push]
    E --> A
    style A fill:#f0f0f0,stroke:#888,color:#111
    style E fill:#1565c0,stroke:#0d47a1,color:#fff
    style F fill:#e8f5e9,stroke:#2e7d32,color:#111
```

## git init — starta ett nytt repo

Förvandlar en vanlig mapp till ett Git-repo. Används när du startar ett helt nytt projekt som inte finns på GitHub än.

```bash
git init
git remote add origin git@github.com:dittnamn/repo-namn.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

`-u origin main` behövs bara den första gången — efteråt räcker `git push`.

## Hela arbetsflödet

```mermaid
flowchart TD
    A["git pull\nhämta det senaste"] --> B["Skriv kod\nändra filer"]
    B --> C["git status\nse vad som ändrats"]
    C --> D["git add filnamn.cs\nförbered för commit"]
    D --> E["git commit -m 'beskrivning'\nspara ögonblicksbild"]
    E --> F["git push\nskicka till GitHub"]
    F --> G["Pull Request\ngranskning och merge"]
    style A fill:#f0f0f0,stroke:#888,color:#111
    style E fill:#1565c0,stroke:#0d47a1,color:#fff
    style F fill:#1565c0,stroke:#0d47a1,color:#fff
    style G fill:#e8f5e9,stroke:#2e7d32,color:#111
```

## .gitignore

En fil i projektets rot som talar om för Git vilka filer som aldrig ska sparas i historiken.

```plaintext
bin/
obj/
.vs/
*.user
.env
secrets.json
```

`bin/` och `obj/` kan vara hundratals megabyte och genereras om automatiskt — ingen anledning att spara dem. `.env` och `secrets.json` kan innehålla lösenord och API-nycklar — om de hamnar på GitHub kan de missbrukas av automatiserade bottar inom minuter.

**Tumregel:** skapa `.gitignore` **innan** din första commit, inte efteråt. Har du råkat commita känsliga filer är de i historiken för alltid — du måste rensa hela historiken, inte bara filen.

## SSH-nyckel

Ett par av filer — en privat (stannar på din dator) och en publik (läggs på GitHub) — som låter dig ansluta till GitHub utan att skriva lösenord varje gång.

```bash
ssh-keygen -t ed25519 -C "din@email.com"
cat ~/.ssh/id_ed25519.pub
ssh -T git@github.com
```

```plaintext
Hi dittnamn! You've successfully authenticated
```

Behövs framför allt om du hanterar mer än ett GitHub-konto på samma dator. En enda inloggning räcker det att logga in via webbläsaren när Git frågar första gången.
