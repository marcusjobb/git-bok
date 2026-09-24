---
title: git init
description: "Förvandla en vanlig mapp till ett Git-repo."
parent: Kommandon
nav_order: 75
---

# git init

Förvandla en vanlig mapp till ett Git-repo.

```bash
git init
```

Skapar en dold `.git/`-mapp i mappen du är i. Det är den mappen som *är* repot — all historik, alla branches, alla commits bor där.

## Nytt projekt, från scratch

```bash
mkdir mitt-projekt
cd mitt-projekt
git init
git remote add origin git@github.com:dittnamn/mitt-projekt.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

## GitHub-alternativet

I praktiken: skapa repot på GitHub först, klona det, jobba i mappen. Då slipper du `git init` och `git remote add` — det är redan ordnat.

```bash
git clone git@github.com:dittnamn/mitt-projekt.git
cd mitt-projekt
# börja jobba direkt
```

## Vad finns i `.git/`?

```plaintext
.git/
├── config          ← repo-specifik konfiguration
├── HEAD            ← vilken branch du är på just nu
├── objects/        ← all data (commits, filer, träd)
└── refs/           ← branches och tags
```

Du behöver aldrig röra det manuellt. Men det är bra att veta att det finns — och att `git clone` skapar exakt samma struktur på din dator som på servern.

## Ta bort Git från en mapp

```bash
rm -rf .git
```

Mappen är en vanlig mapp igen. Hela historiken är borta. Kör inte detta om du inte menar det.
