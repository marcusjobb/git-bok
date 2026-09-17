---
title: Rebase gick fel
parent: Scenarios
nav_order: 50
---

# Rebase gick fel

Rebase är kraftfullt. Det är också det kommando som flest personer stör till på ett sätt som känns oöverskådligt.

Det goda: det finns nästan alltid en väg tillbaka.

## Avbryta en pågående rebase

Är du mitt i en rebase med konflikter och vill inte fortsätta?

```bash
git rebase --abort
```

Du är tillbaka till exakt läget innan rebasen startade. Ingenting förändrat.

## Rebasen gick igenom men resultatet är fel

Du körde `git rebase main` och det verkar ha gått igenom — men historiken ser konstig ut, eller koden är fel.

Git sparar positionen innan rebasen i `ORIG_HEAD`:

```bash
git reset --hard ORIG_HEAD
```

Tillbaka till läget precis innan rebasen. `ORIG_HEAD` skrivs över av nästa destruktiva operation, så agera snabbt.

## Rebasen pågår men du är vilsen i konflikter

Rebase spelar av commits en i taget och pausar vid varje konflikt. Om du inte vet var du är:

```bash
git status
```

```plaintext
interactive rebase in progress; onto 9d2e1f0
Last command done (2 commands done):
   pick a3f8c21 feat: rabattkod-input

You are currently rebasing branch 'feature/rabattkod' on '9d2e1f0'.
  (fix conflicts and then run "git rebase --continue")
```

Git berättar precis var du är. Lös konflikten i den utpekade filen:

```bash
# redigera filen
git add Kassan.cs
git rebase --continue
```

Upprepa tills rebasen är klar.

## Rebasade en delad branch av misstag

Det värsta scenariot. Du körde `git rebase` på en branch som kollegor arbetar på — nu har alla divergerande historik.

**Steg 1:** Varsla teamet direkt. De behöver veta.

**Steg 2:** Återställ branchen till läget innan rebasen med reflog.

```bash
git reflog | head -20
```

Hitta entry:n precis innan rebasen startade (letar efter `rebase (start)` eller senaste commit-hash på branchen):

```plaintext
a3f8c21 HEAD@{0}: rebase (finish): returning to refs/heads/feature/rabattkod
...
b5c2d1e HEAD@{4}: commit: feat: sista committen innan rebasen
```

```bash
git reset --hard b5c2d1e
git push --force-with-lease
```

**Steg 3:** Teammedlemmar som hämtat den gamla versionen behöver:

```bash
git fetch
git reset --hard origin/feature/rabattkod
```

## Kom ihåg till nästa gång

Rebase är säkert på din egna lokala branch, innan du pushat eller delar den. Så fort en branch finns på remote och andra kan ha hämtat den — använd merge istället.
