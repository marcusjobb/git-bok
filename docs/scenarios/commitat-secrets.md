---
title: Råkade commita secrets
description: "Råkade commita secrets i Scenarios — Git-boken av Marcus Ackre Medina"
parent: Scenarios
nav_order: 30
---

# Råkade commita secrets

Du har precis committat — och insett att `appsettings.json` innehöll ett riktigt lösenord. Eller en API-nyckel. Eller en connectionstring med credentials i klartext.

Andas. Sedan agerar du snabbt.

## Steg 0: Är det redan pushat?

Det är den avgörande frågan.

```bash
git status
git log --oneline origin/main..HEAD   # commits lokalt som inte finns på remote
```

Om kommandot ger output: committen finns bara lokalt. Du har tid.
Om det är tomt: den är pushad. Gå direkt till "Redan pushad".

---

## Inte pushad — enklaste fallet

**Ta bort filen från historiken och staga om:**

```bash
git rm --cached appsettings.json       # ta bort från staging, behåll lokalt
echo "appsettings.json" >> .gitignore  # se till att den aldrig committas igen
git add .gitignore
git commit --amend --no-edit           # lägg till .gitignore i samma commit, ta bort secrets
```

Rotera nyckeln ändå. `--amend` skriver om den lokala committen men det finns ingen garanti på att ingen sett den under de minuter den funnits.

---

## Redan pushad — allvarligare

Secrets i en pushad historik måste hanteras i två steg: **rensa historiken** och **rotera nyckeln**.

### Steg 1: Rotera nyckeln — gör det nu

Innan du gör något annat: gå till tjänsten där nyckeln hör hemma och inaktivera den. GitHub, Azure, AWS, Stripe — alla har ett ställe där du kan rulla en ny nyckel och inaktivera den gamla.

En angripare behöver bara sekunder. Bots skannar konstant GitHub efter nycklar.

### Steg 2: Rensa historiken med git filter-repo

```bash
pip install git-filter-repo

git filter-repo --path appsettings.json --invert-paths
```

`--invert-paths` tar bort filen från hela historiken — varje commit. Det är en destruktiv operation som skriver om alla commit-hashar.

### Steg 3: Force push

```bash
git push --force-with-lease
```

Varna teamet — alla som klonat repot måste göra `git fetch` och `git reset --hard origin/main` (deras lokala historik stämmer inte längre).

### Steg 4: Begär cache-rensning på GitHub

GitHub cachat innehåll. Gå till GitHub Support och begär att de rensar cachen för repot.

---

## Det bästa skyddet: commit inte secrets alls

Konfigurera `.gitignore` innan första commit:

```plaintext
appsettings.*.json          ← alla miljöspecifika settings
!appsettings.json           ← men tillåt baskonfigurationen (utan credentials)
*.env
.env.*
secrets.json
```

Och använd environment variables eller Azure Key Vault / AWS Secrets Manager för riktiga credentials — inte filer i repot.

---

> **Kom ihåg:** Om en nyckel har sett dagsljus i ett Git-repo — oavsett hur kort tid — behandla den som komprometterad. Rotera alltid.
