---
title: Återställa förlorad kod
description: "Du körde git reset --hard. Eller rebaser gick fel. Eller du tappade en branch. Koden verkar borta."
parent: Scenarios
nav_order: 70
---

# Återställa förlorad kod

Du körde `git reset --hard`. Eller rebaser gick fel. Eller du tappade en branch. Koden verkar borta.

Den är troligtvis inte det.

## git reflog — Git minns allt

`git reflog` visar varje gång HEAD rört sig — commits, resets, checkouts, rebaser. Allt:

```bash
git reflog
```

```plaintext
a3f8c21 HEAD@{0}: reset: moving to HEAD~3
9d2e1f0 HEAD@{1}: commit: feat: lägg till rabattkod-validering
7b4a3c8 HEAD@{2}: commit: fix: typo i felmeddelande
b5c2d1e HEAD@{3}: commit: feat: rabattkod-input i kassan
```

`HEAD@{1}`, `HEAD@{2}`, `HEAD@{3}` — de commits som försvann när du körde `reset --hard HEAD~3`.

## Återställ till ett tidigare läge

```bash
git reset --hard HEAD@{3}
```

Du är tillbaka. Alla tre commits finns igen.

Eller, om du vill säkra koden på en ny branch utan att röra det du är på:

```bash
git checkout -b räddad-branch HEAD@{3}
```

## Tappade en branch

Tappade du en hel branch som inte var mergad?

```bash
git reflog | grep "checkout: moving from"
```

```plaintext
b5c2d1e HEAD@{5}: checkout: moving from feature/rabattkod to main
```

Sista committen på branchen innan du bytte: `b5c2d1e`.

```bash
git checkout -b feature/rabattkod b5c2d1e
```

Branchen är tillbaka.

## Reflog har en tidsgräns

Git sparar reflog i 90 dagar som standard. Efter det är posten borta — och då är koden faktiskt borta.

90 dagar är lång tid. De flesta "jag tappade koden"-situationer händer för minuter eller timmar sedan, inte månader.

## Om reflog inte räcker

En sista utväg: `git fsck`.

```bash
git fsck --lost-found
```

Det söker igenom Git-objektdatabasen efter "dangling commits" — commits som inte längre refereras av någon branch eller tag men fortfarande finns i `.git/objects/`.

```plaintext
dangling commit a3f8c21d4e9b7f2a1c0d5e8f3b6a9c2d4e7f1b0a
```

```bash
git show a3f8c21d    # kolla om det är rätt
git checkout -b återhämtad a3f8c21d
```

Det är den verkliga sista plankan. Men den fungerar.
