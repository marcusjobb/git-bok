---
title: git clone
description: "git clone i Kommandon — Git-boken av Marcus Ackre Medina"
parent: Kommandon
nav_order: 80
---

# git clone

Kopiera ett repo till din dator — med hela historiken.

```bash
git clone git@github.com:marcusjobb/git-bok.git
```

Skapar en mapp med repo-namnet (`git-bok/`) och sätter automatiskt upp `origin` att peka på källan.

## Klona till specifikt mappnamn

```bash
git clone git@github.com:marcusjobb/git-bok.git min-git-bok
```

## Klona bara senaste commit (shallow clone)

```bash
git clone --depth 1 git@github.com:marcusjobb/git-bok.git
```

Hämtar bara den senaste snapshoten utan historik. Mycket snabbare för stora repos, men du kan inte köra `git log` eller bläddra i historiken. Bra för CI/CD-pipelines som bara behöver bygga koden.

## HTTPS vs SSH

```bash
# HTTPS — frågar om lösenord (eller token)
git clone https://github.com/marcusjobb/git-bok.git

# SSH — kräver SSH-nyckel, men frågar aldrig om lösenord
git clone git@github.com:marcusjobb/git-bok.git
```

Föredra SSH — sätter du upp nyckeln en gång slipper du autentisering varje push och pull. Se [Vanliga kommandon](../grunder/vanliga-kommandon.md) för hur du sätter upp SSH-nyckel.
