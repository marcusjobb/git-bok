---
title: Testa dig själv
description: "Testa dig själv i Scenarios — Git-boken av Marcus Ackre Medina"
parent: Scenarios
nav_order: 999
---

# Testa dig själv — Scenarios

Det enda sättet att lära sig hantera kaos är att öva i kontrollerat kaos. Allt det här går att återskapa i ett testmiljö-repo.

**Skapa testmiljön en gång:**

```bash
mkdir git-scenarios && cd git-scenarios
git init
echo "start" > fil.txt
git add fil.txt && git commit -m "init"
```

---

## Scenario 1 — Du committade på fel branch

Skapa situationen:

```bash
# Se till att du är på main (utan att ha skapat en feature-branch)
echo "ny funktion" >> fil.txt
git add fil.txt
git commit -m "feat: ny funktion"
```

Committen hamnade på `main` — men den borde vara på `feature/ny-funktion`. Hur fixar du det?

*Tips om du fastnar: kolla `cherry-pick` och `reset`.*

---

## Scenario 2 — Secrets råkade med i en commit

Skapa situationen:

```bash
echo "DB_PASSWORD=supersecret123" > .env
git add .env
git commit -m "add config"
```

Frågor att besvara:
1. Är committen pushad eller inte? Hur kontrollerar du?
2. Hur tar du bort `.env` från **staging area** utan att ta bort filen lokalt?
3. Vad är det allra första du bör göra om nyckeln redan är pushad och exponerad?

---

## Scenario 3 — Merge-konflikten som inte vill lösa sig

Skapa situationen:

```bash
git switch -c feature/a
echo "version A" > konflikt.txt
git add konflikt.txt && git commit -m "version A"

git switch main
echo "version B" > konflikt.txt
git add konflikt.txt && git commit -m "version B"

git merge feature/a
```

Nu har du en konflikt. Lös den manuellt (öppna filen, välj rätt version, ta bort konfliktmarkörerna) och avsluta mergen.

---

## Scenario 4 — Rebase röran

Skapa situationen:

```bash
git switch -c feature/b
echo "rad 1" >> fil.txt && git add fil.txt && git commit -m "rad 1"
echo "rad 2" >> fil.txt && git add fil.txt && git commit -m "rad 2"

git switch main
echo "main-ändring" >> fil.txt && git add fil.txt && git commit -m "main-ändring"

git switch feature/b
git rebase main
```

Om det uppstår konflikter — lös dem och kör `git rebase --continue`. Om det kör iväg: `git rebase --abort` tar dig tillbaka till läget innan rebase.

---

## Scenario 5 — Hitta buggen (bisect)

Skapa en historik med en "bugg" inbäddad:

```bash
for i in 1 2 3 4 5; do
  echo "commit $i" >> logg.txt
  [ $i -eq 3 ] && echo "BUG" >> logg.txt
  git add logg.txt && git commit -m "commit $i"
done
```

Nu vet du att "BUG" finns någonstans i historiken. Använd `git bisect` för att hitta exakt vilken commit som introducerade den.

*Ledtråd: `git bisect start`, `git bisect bad`, `git bisect good <hash>`, och `git bisect reset` när du är klar.*

---

## Scenario 6 — Återskapa förlorad kod via reflog

Skapa situationen — och förstör sedan medvetet:

```bash
echo "viktig kod" >> viktig.txt
git add viktig.txt && git commit -m "viktig commit"

# Ångra committen hårt — koden verkar försvunnen
git reset --hard HEAD~1
```

Koden är "borta". Återskapa den med `git reflog`.

---

## Quiz — Sant eller falskt?

1. `git reset --hard` kan återskapa commits som tappats med `git reflog`.
2. Om du råkat commita ett lösenord som redan är pushat räcker det att ta bort filen i nästa commit.
3. En merge-konflikt uppstår alltid när två branches ändrat exakt samma rad.
4. `git rebase --abort` är alltid säkert att köra.
5. `git bisect` kräver att du vet vilken commit som introducerade buggen.
