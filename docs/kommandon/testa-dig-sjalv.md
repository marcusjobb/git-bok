---
title: Testa dig själv
description: "Testa dig själv i Kommandon — Git-boken av Marcus Ackre Medina"
parent: Kommandon
nav_order: 999
---

# Testa dig själv — Kommandon

Inga facit på nästa sida. Det är meningen.

---

## Del 1 — Sant eller falskt?

Kolla svaret genom att faktiskt köra kommandot i en terminal.

1. `git status` ändrar något i repot.
2. `git add .` lägger till alla filer — inklusive de i `.gitignore`.
3. `git commit` skickar din kod till GitHub.
4. `git stash pop` tar bort den sparade stashen och lägger tillbaka ändringarna.
5. `git log --oneline` visar samma information som `git log`, men kortare.
6. `git revert` tar bort en commit från historiken.
7. `git fetch` uppdaterar dina lokala filer.
8. `git diff` visar skillnaden mellan din working directory och staging area.

---

## Del 2 — Fyll i blanket

Vilket kommando ska in?

```bash
# Skapa en ny branch som heter "feature/login" och byt till den direkt
git _______ -c feature/login

# Se vem som ändrade rad 42 i Program.cs
git _______ -L 42,42 Program.cs

# Ångra den senaste committen men behåll ändringarna i working directory
git _______ --soft HEAD~1

# Spara undan halvfärdig kod utan att committa
git _______

# Hämta ändringar från remote utan att mergea dem
git _______
```

---

## Del 3 — Vad händer?

Beskriv vad varje kommando gör, utan att köra det. Kör det sedan och kontrollera om du hade rätt.

```bash
git log --oneline --graph --all
```

```bash
git diff HEAD~2 HEAD -- Program.cs
```

```bash
git stash list
```

```bash
git cherry-pick abc1234
```

---

## Del 4 — Ordna i rätt ordning

Steg för att skapa en ny feature och pusha den. Sätt i rätt ordning:

- `git push -u origin feature/rabattkoder`
- `git add Rabattkod.cs`
- `git switch main && git pull`
- `git switch -c feature/rabattkoder`
- `git commit -m "feat: lägg till rabattkod-validering"`

---

## Del 5 — Rätta Pelles commit-meddelanden

Pelle har skrivit dessa commit-meddelanden. Vad är problemet med vart och ett, och hur hade du skrivit det bättre?

1. `git commit -m "fix"`
2. `git commit -m "uppdatering"`
3. `git commit -m "äntligen"`
4. `git commit -m "Lade till ny klass för att hantera alla olika typer av rabattkoder som kan appliceras på en kundvagn i kassan"`
5. `git commit -m "WIP"`

---

## Del 6 — Skapa ett testmiljö-repo

Kör det här en gång — du behöver det för scenariosidan också.

```bash
mkdir git-testmiljo && cd git-testmiljo
git init
echo "# Test" > README.md
git add README.md
git commit -m "init: första commit"
```

Nu du har en lekplats. Testa kommandona i Del 2 härifrån.
